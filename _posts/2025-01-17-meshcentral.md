---
title: "MeshCentral"
date: 2025-01-17 23:44:00 -0400
description: "An experiment in self-hosted remote desktop software"
tags: [Computers, Technology, MeshCentral, Homelab]
image: https://i.postimg.cc/g2Cn3sVV/Mesh-Central.png
---

<style>
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
        width:50%;
        overflow:hidden;
        }
    .flex33{
        padding-top: 35px;
        padding-left: 8px;
        padding-right: 8px;
        height: 175px;
    }
    .clear {
        clear:both;
        height:1.2em;
        margin-bottom:-1px;
    }
</style>

A few weeks ago my good friend Sneakr told me about MeshCentral: a free open-source remote desktop control service with a mesh agent that can be self-hosted.  I've been interested in something like this for a long time because, like so many other users, I have had numerous run-ins with TeamViewer and AnyDesk claiming I'm using their software for commercial use despite the fact that 1) I'm not, and 2) the machines I'm remote controlling are in my own house on the same network.  A simple IP check would confirm the second part.  About 3-4 years ago when I last used TeamViewer I actually went through their appeal process thinking if it were approved their system would at least have it on record that I was remote controlling computers in my own home.  This worked for all of a month.  AnyDesk was a nice reprieve but even they went the same direction.  Worse actually because their implementation would let me connect to a remote machine but then display their nag screen with a two-minute timer.

<div class="div50"><img src="https://i.postimg.cc/2jGGTbXb/teamviewer-timeout.png" alt=""></div>
<div class="div50"><img src="https://i.postimg.cc/gk0D7zfM/Any-Desk-warning.jpg" alt=""></div>
<div class="clear"></div>

This is just a money grab IMHO and AnyDesk isn't even trying to hide it.  I did find a script on Github that generates a new ID for the controlling computer and this worked as a technically viable workaround since I could go several months before having to run the script again.  But this was a short-term solution for a long-term problem.  Knowing the industry it would just be a matter of time before this workaround would be classified as an exploit and patched.  Enter MeshCentral.  Since you self-host the mesh agent and all connections are done internally, between that and the software itself being licensed under [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0), warnings about my usage would finally be a thing of the past.

Setting it up was a little more involved than I'm used to, but I did get it working after just a little while.  In the grand scheme of things there isn't much software that has documentation specifically for LXC containers, however I've found that unless you're working with something specifically written for Docker (I find this to be incredibly limiting, personally) if something can be installed on either Debian or Ubuntu Linux, it can generally be installed in an LXC container.  Since [MeshCentral's documentation](https://meshcentral.com/docs/MeshCentral2InstallGuide.pdf) covered installing on Ubuntu, I created an LXC container with an Ubuntu CT template, a single CPU core, 512MB of RAM, and 2GB of drive space.  Then it was time to install things.

![MC_LXC](https://i.postimg.cc/XJcRsjTj/MC_Resources.png)

MeshCentral requires the Universe repository be enabled and also depends on NodeJS and NPM (Node Package Manager).

```bash
sudo add-apt-repository universe
sudo apt update
sudo apt install nodejs -y
sudo apt install npm -y
```

The documentation also recommends verifying installation of NodeJS and NPM by using the following:

```bash
node -v
npm -v
```

```bash
root@MeshCentral:~# node -v
v18.19.1

root@MeshCentral:~# npm -v
9.2.0
```

If you're using MeshCentral to control a lot of devices (e.g. over 100) the documentation has instructions for installing MongoDB before proceeding further.  This didn't apply to me so I continued on.

MeshCentral then requires permission to listen to ports below 1024 since those are reserved for the root user.  Since on an LXC container there is only the root user unless you create additional users this step may not have been required, but I ran it anyway.

```bash
whereis node
node: /usr/bin/node /usr/include/node /usr/share/man/man1/node.1.gz
sudo setcap cap_net_bind_service=+ep /usr/bin/node
```

Next was using NPM to install MeshCentral.

```bash
npm install meshcentral
```

Once complete MeshCentral was ready to be started.

```bash
node ./node_modules/meshcentral
```

```bash
root@MeshCentral:~# node ./node_modules/meshcentral
MeshCentral HTTP redirection server running on port 80.
MeshCentral v1.1.38, LAN mode.
MeshCentral HTTPS server running on port 443.
```

![MC_FirstLogin](https://i.postimg.cc/8PC2bVwG/MC_FirstLogin.png)

Logging in was easy and fast, but this is where things got a little tricky for me.  I created a device group which went just fine, but the default method to add a client to MeshCentral is to click "Add Agent" and then select the relevant options which then results in an installer be downloaded which can then be distributed to each client you wish to control.  Well that last part didn't work for some reason.  The download would try to start but I would get an instant download failure message no matter which web browser I was using.  

![MC_Devices](https://i.postimg.cc/MHH91zwr/MC-Add-Agent.png)

I eventually found a workaround where if I clicked on my user profile, then the device group I created, and finally "Invite" I got a URL that I could copy and then paste into the web browser of each client.

<div class="div50"><img src="https://i.postimg.cc/JhgNSjCK/MC-Device-Group.png" alt=""></div>
<div class="div50"><img src="https://i.postimg.cc/8CGwtRDv/MC-Invite.png" alt=""></div>
<div class="clear"></div>

This worked on all but one of my Windows VMs that I needed to control remotely.  The one that didn't work was Windows 11 24H2 because MeshCentral relies on Windows Management Instrumentation Command-Line (WMIC) to install and because WMIC is being deprecated, in Win11 24H2 it is disabled by default.  Enabling this in Optional Features under Windows Settings -> System.  Like with anything vaguely resembling Windows Update, this process took way longer than it had any right to.  But once installed I could then add the VM to MeshCentral without issue.

In testing the remote connection everything was pretty solid.  I didn't encounter any connection issues or difficulties when connecting to a client, nor did I encounter any disconnects, lagging, or other hindrances.  There was only one problem I did run into which was a design limitation of MeshCentral: you can only connect to the mesh server in a web browser, no client application exists.  Because of this, certain keyboard and mouse functions such as back and forward mouse buttons, alt-tab, and F5, aren't passed through to the client.  While it certainly falls under #FirstWorldProblems, this is something of a step backward for me in terms of workflow efficiency.  Because of this I ultimately decided against using MeshCentral long term.  Don't get me wrong I'd still give MeshCentral a four out of five easily because the only real problem I encountered was downloading the mesh agent executable and I'm thinking that was a glitch more than anything else.  If the devs do one day make a control client that fulfills my workflow needs I will definitely consider coming back to MeshCentral because I do like the setup and freedom from overly needy paid clients.