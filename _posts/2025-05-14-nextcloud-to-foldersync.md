---
title: "Goodbye Nextcloud, Hello FolderSync"
date: 2025-05-14 19:38:00 -0400
description: "Nextcloud's Android app sucks, can FolderSync relieve the headaches?"
tags: [Computers, Technology, Android, Nextcloud, FolderSync, Homelab]
image: https://i.postimg.cc/0ND6MWyz/Folder-Sync-Logo.png
---

<style>
    .center {
    margin: auto;
    width: 450px;
  	}
    .div25 {
        float:left;
        padding: 10px 8px;
        height:150px;
        width:25%;
        overflow:hidden;   
    }
    .div33 {
        float:left;
        padding: 10px 8px;
        height:175px;
        width:33%;
        overflow:hidden;
        }
    .div50 {
        float:left;
        padding: 10px 8px;
        height:200px;
        width:200px;
        overflow:hidden;
        }
    .clear {
        clear:both;
        height:1.2em;
        margin-bottom:-1px;
    }
</style>

Back in 2021 I experimented with SyncThing on my previous NAS.  The setup process was pretty clunky and it took me a few tries to get it working, but I was eventually successful.  This was how I backed up my SMS and call log backups weekly from my phone to my NAS.  Eventually I included my photos and music folders.  However this was really just a one-way backup sync, I wasn't using it to update anything on my phone.  The main reason things were just one-way is that at the time I was still storing most of my personal files on my desktop, I hadn't yet migrated things to my NAS.  Fast forward to mid-2023 and I started messing around with Nextcloud as a replacement for SyncThing and setup at least was a lot easier.  Honestly the only hard part I had with setting up the Nextcloud LXC container was enabling active scanning of the mounted file systems so that Nextcloud would update its database whenever I added anything via Samba (SMB) instead of the Nextcloud web UI or Android app.  That was my edge case for Nextcloud: have the files also accessible via SMB share.  Why do this?  So I didn't have to use the web UI on my desktop to access my files.  A good example was when viewing photos, viewing them in my preferred photo viewer (XnView) literally took less than 1/10th the time as going through my web browser.  Nextcloud was really just serving as an authenticator while the Android app was doing all of the syncing, and even then it was only over WiFi or with a VPN enabled since I don't expose any of my self-hosted services.  So why retire Nextcloud?

To give the Nextcloud Android app some credit where it's due, the app at least *did* work.  But that's pretty much the end of my positive feedback.  As of writing this there's no sync scheduling and the manual sync option rarely, and I mean *rarely*, ever initiates a sync operation.  While it was nice that it had the option to instantly detect local changes to the files (compared to a scheduled detection for file changes), about half of the time there was usually a five-minute delay (like after taking a picture) and the other half of the time it would randomly initate the sync later in the day.  I did verify that being on my home WiFi or VPN over mobile data made no difference.  Whether the developers just lacked the skill to build a polished Android app or just didn't care, the end result was still the same.  Personally I'm leaning towards Column B because, according to a plethora of anecdote, the iOS app is considerably worse and almost never gets updated.  But during the time I was using Nextcloud on Android my primary concern was backing up what was on my phone to self-hosted storage, and I wasn't really modifying the files being sync'd, so I lived with its limitations for a while.  But with my recent increase in free time I revisted this setup by first debating if the Nextcloud server, or any kind of password-based authentication server was even necessary.  Since I haven't ever exposed any of my services, nor do I plan to, the answer to this question was "no".  With that, just hosting an SMB share became the plan.  For file/folder syncing, that's where FolderSync comes in.

A *very* long time ago I used FolderSync for a brief time to back up my SMS backups and call logs.  That fact alone should tell you how long I've had the SMS Backup and Restore app on my phones, lol.  Like with SyncThing and Nextcloud, the app worked, but back then the app was so new that the UI layout and functionality wasn't quite where it needed to be for my needs.  But in the time that has passed, a lot of changes and improvements have been made and I'm very pleased with the app's evolution.  FolderSync operates by creating "folder pairs" where you select a folder on your device and then a remote folder and then the app syncs the folder contents.  The remote services supported is quite extensive but what sold me on this app (no I haven't ever paid for it) way back when and also now is that it supports file protocols as well as cloud services, specifically SMB.  It also supports FTP, sFTP, S3, and WebDAV.  Ironically it can also interface with Nextcloud, but as I said before, I don't see the need for an authentication service when SMB supports password authentication and no connections are over public internet connections.  Were this not the case, I would be trying FolderSync while keeping the Nextcloud server operating.

Container creation was almost the simplest I've ever done since there are only three main parts to what I did: Mount external storage, install Samba, configure Samba.  No seriously that's all that I needed to do.  For the LXC container in Proxmox I chose the Debian 12 template and allocated 1GB of virtual disk storage, 1 CPU core, and 512MB of RAM.  Once created I edited the LXC config file in nano to add the mount points for ZFS folders I wanted to attach to the container.

```bash
mpX: /path_to_ZFS_folder,mp=/mnt/[foldername]
# repeat this for each folder to be mounted
```

![LXC Config](https://i.postimg.cc/26dckcwF/LXC-SMB.png){: data-gallery="gallery1"}

Next I needed to change ownership and permissions of the folders for each mount point so that the Samba users would have write access to each share.  I ran the following from a terminal in Proxmox.

```bash
chown -R 101000:101000 [folder for User1]
chmod -R 755 [folder for User1]
chown -R 101001:101001 [folder for User2]
chmod -R 755 [folder for User2]
chown -R 101002:101002 [folder for User3]
chmod -R 755 [folder for User3]
# repeat this for each folder to be mounted
```

The 101000 user name (and each digit higher) corresponds to the numerical value of the user inside the container.  Root is user 0 so a folder that requires root access would have a user value of 100000 (one hundred thousand).  The first non-root user created in Linux has a number of 1000 so the corresponding number for that is 101000 (one hundred one thousand) with each user created after that increasing the last digit by one.  Setting the permissions this way distinguishes the users in Proxmox (including root) from the users inside the container so the container can run unprivileged (default setting).  If a container were compromised where someone obtained root access to the container and somehow obtained access beyond the mounted storage, they wouldn't be able to change any data because they wouldn't have permission.  Root inside the container is not the same root as in Proxmox even though they have the same name.  I knew in advance which user names inside the LXC container would be associated with the ownership values I used, but if I didn't, or I had already created the accounts in the container, I would just use `cat /etc/passwd` which then prints the user names with ID numbers.

With the folders ready I could then start the container.  Like with any installation the first step was running `apt update`.  With that done I created the three user accounts I needed for the share.

```bash
adduser [username]
```
```bash
Adding user `[username]' ...
Adding new group `[username]' (1001) ...
Adding new user `[username]' (1001) with group `[username]' ...
Creating home directory `/home/[username]' ...
Copying files from `/etc/skel' ...
New password: 
Retype new password: 
passwd: password updated successfully
Changing the user information for [username]
Enter the new value, or press ENTER for the default
        Full Name []: 
        Room Number []: 
        Work Phone []: 
        Home Phone []: 
        Other []: 
Is the information correct? [Y/n] y
# repeat this for each user account to be created
```

Next was installing Samba and giving each user account a Samba password:

```bash
apt install samba
```
```bash
smbpasswd -a [username]
```

With samba installed and the user accounts ready it was time to create the Samba shares by editing the `/etc/samba/smb.conf` file in nano and adding a block at the end of the file for each share.

```bash
[Share name]
path = /path_to_folder/[folder name]
browsable = yes
read only = no
guest ok = no
writable = yes
valid users = user1
# repeat this for each SMB share
```

All that was needed now was to restart Samba and then the shares were active.

```bash
service smbd restart
```

In FolderSync the first step was to add the Samba shares to the accounts tab.  For me that was two shares, one that contained the backup folders for my Phone, and another for other personal data (e.g. Obsidian vaults).

<div class="center">
<div class="div50"><img src="https://i.postimg.cc/bY45xBCg/Screenshot-2025-05-27-01-47-12-79.jpg" alt="" data-gallery="gallery2"></div>
<div class="div50"><img src="https://i.postimg.cc/tCPM2N8j/Screenshot-2025-05-26-23-56-39-42-d34a4a90c4bafa19d6180fac09c8c8af.jpg" alt="" data-gallery="gallery2"></div>
<div class="clear"></div></div>

Next was creating the folder pairs.

<div class="center">
<div class="div50"><img src="https://i.postimg.cc/qB568Cfn/IMG-20250527-023012.jpg" alt="" data-gallery="gallery3"></div>
<div class="div50"><img src="https://i.postimg.cc/W1wfPb2Y/Screenshot-2025-05-26-23-36-03-54-d34a4a90c4bafa19d6180fac09c8c8af.jpg" alt="" data-gallery="gallery3"></div>
<div class="clear"></div></div>

Once each folder pair was created I could then set the sync schedule and other options, the one category of features that was glaringly missing from Nextcloud.  I haven't shown all of the options, but you really do get to configure a lot.  I always love it when I get the kitchen sink.

<div class="div33"><img src="https://i.postimg.cc/k5gtQN5Q/Screenshot-2025-05-28-15-10-09-28-d34a4a90c4bafa19d6180fac09c8c8af.jpg" alt="" data-gallery="gallery4"></div>
<div class="div33"><img src="https://i.postimg.cc/9fgwJ44v/Screenshot-2025-05-28-15-10-19-35-d34a4a90c4bafa19d6180fac09c8c8af.jpg" alt="" data-gallery="gallery4"></div>
<div class="div33"><img src="https://i.postimg.cc/mgwH1pTZ/Screenshot-2025-05-28-15-11-08-46-d34a4a90c4bafa19d6180fac09c8c8af.jpg" alt="" data-gallery="gallery4"></div>
<div class="clear"></div>

And that's it.  Everything is set up and after using it for a week everything has been working smoothly.  Having the instant sync enabled for my music folder and Obsidian vault has been very nice - no waiting or manual syncing.  As yet I haven't encountered any drawbacks or issues with this setup so this is likely how I'll be syncing my mobile files for the foreseeable future.  FolderSync also makes a Windows version of their app which would come in handy for syncing bookmarks between my desktops and laptop without having to rely on Google accounts or Brave's sync service, however it costs $28 for a license and there is no free option, just a free 2-week trial.  Since I'd just be using it for personal use, I can't justify spending that on a sync app.  Maybe if I don't soon find a free open-source option I'll revisit SyncThing to see if that's easier to set up than I remember.

Back to my other forms of digital mayhem.  See you around!