---
# the default layout is 'page'
icon: fas fa-flask
order: 6
---
<style>
  .column {width:50%; float: left;}
  p {margin-bottom:0;}
  li {line-height:1;}
  p.clear {clear: both;}
</style>

<div class="column">
  <h3 style="text-align: left">Network Stack Hardware:</h3>
    <p>Arris Surfboard SB8200</p><ul>
        <li>DOCSIS 3.1</li>
        <li>Dual 1GbE ports with Link Aggregation support</li></ul>
    <p>Dell PowerEdge R210 ii</p><ul>
        <li>Intel Xeon E3-1220 v2 4-core 3.1GHz</li>
        <li>16GB ECC DDR3</li>
        <li>60GB SATA SSD</li></ul>
    <p>Dell PowerConnect 6224</p><ul>
        <li>24x GbE ports</li></ul>
    <p>2x Ubiquiti UAP-AC-Pro</p><ul>
        <li>48VDC PoE</li>
        <li>1300Mbps max throughput</li>
        <li>VLAN and meshing support</li></ul>
    <p>8-outlet Individual Switched PDU Strip</p><ul>
        <li>Allows for streamlined power cycling of network stack components</li></ul>
    <p>CyberPower OR700LCDRM1U UPS</p><ul>
        <li>700VA/400W max power output</li>
        <li>Sufficient to run network stack for 1 hour during power loss</li></ul>
</div>
<div class="column">
  <h3 style="text-align: left">Network Stack Software:</h3>
    <p>pfSense Firewall</p><ul>
        <li>FreeBSD based</li>
        <li>pfBlockerNG</li>
        <li>Assigns VLANs to IoT devices</li>
        <li>Enforces sleep schedule for applicable devices</li></ul>
</div>
<p class="clear"></p>

<div class="column">
  <h3 style="text-align: left">Proxmox Server Hardware:</h3>
    <p>Dell PowerEdge R730XD</p><ul>
        <li>Intel Xeon E5-2690 v4 14-core 2.6GHz</li>
        <li>128GB ECC DDR4</li>
        <li>24x 2.5" SAS3 front hotswap bays</li>
        <li>2x 2.5" SAS3 rear hotswap bays</li>
        <li>2x 750W 80+ Platinum power supplies</li>
        <li>2x 10GbE SFP+ 2x 1GbE mezzanine daughter card</li>
        <li>2x 400GB SAS3 SSDs in ZFS mirror</li>
        <li>2x 1.92TB SAS3 SSDs in ZFS mirror</li>
        <li>4x 3.84TB m.2 NVMe SSDs in ZFS RAID10</li>
        <li>6x 3.84TB SATA SSDs in various ZFS configurations</li></ul>
  <h3 style="text-align: left">Proxmox Virtual Machines:</h3>
    <p>Windows 10 22H2</p><ul>
        <li>Work VM for software testing</li></ul>
    <p>Windows 10 22H2 (32-bit)</p><ul>
        <li>Work VM for legacy software testing</li></ul>
    <p>Windows 11 23H2</p><ul>
        <li>Work VM for software testing</li></ul>
    <p>Windows 11 24H2</p><ul>
        <li>Work VM for software testing</li></ul>
    <p>MacOS 12 Monterey</p><ul>
        <li>Work VM for software testing</li></ul>
    <p>Windows 10 22H2</p><ul>
        <li>Personal VM for testing Windows mods and suspicious software</li></ul>
  <h3 style="text-align: left">Proxmox Misc:</h3>
    <p>ISO Storage</p><ul>
        <li>OS installer ISOs and LXC container templates</li>
        <li>Uses 1.92TB ZFS mirror for data storage</li></ul>
    <p>VM and LXC backups</p><ul>
        <li>Full backups created after initial setup and at key restoration points</li>
        <li>Performed manually as needed</li>
        <li>Uses third 3.84TB ZFS mirror for backup storage</li></ul> 
</div>
<div class="column">
  <h3 style="text-align: left">Proxmox LXC Services:</h3>
    <p>Served via ZFS RAID10 pool</p>
    <p>Tailscale</p><ul>
        <li>VPN connection to home network</li>
        <li>Uses WireGuard for VPN connections</li>
        <li>Primarily used to provide mobile connection to personal cloud</li></ul>
    <p>UniFi Controller</p><ul>
        <li>Provisions and monitors WiFi access points</li></ul>
    <p>RustDesk</p><ul>
        <li>Debian 12 template</li>
        <li>Self-hosted relay server</li>
        <li>Provides remote desktop to all Proxmox Windows and MacOS VMs</li></ul>
    <p>Homepage</p><ul>
        <li>Self-hosted dashboard to all homelab services</li></ul>
    <p>AMP (Application Management Panel)</p><ul>
        <li>Game server hosting</li>
        <li>Terraria</li>
        <li>Valheim</li>
        <li>7 Days to Die</li>
        <li>Satisfactory</li></ul>
    <p>Samba file server 1 (inactive but operational)</p><ul>
        <li>Debian 12 template</li>
        <li>Serves test files, software, and storage for work</li>
        <li>Uses 3.84TB ZFS mirror for data storage</li></ul>
    <p>Samba file server 2</p><ul>
        <li>Debian 12 template</li>
        <li>Hosts Samba shares for personal files and Android device backups</li>
        <li>Uses 7.68TB ZFS stripe mirror for data storage</li></ul>
    <p>Immich</p><ul>
        <li>Debian 12 template</li>
        <li>Runs without Docker</li>
        <li>Syncs and stores all Android device photos, videos, and downloaded audiovisual content</li>
        <li>Machine learning and facial recognition enabled</li></ul>
    <p>*arr</p><ul>
        <li>Prowlarr</li>
		<li>Radarr</li>
		<li>Sonarr</li>
		<li>Lidarr</li>
		<li>Readarr</li>
		<li>Jackett</li>
		<li>FlareSolverr</li></ul>
    <p>DeepSeek</p><ul>
        <li>Debian 12 template</li>
        <li>Runs using command line Ollama (might try to use a web UI frontend if a self-hosted version becomes available)</li>
        <li>Exploratory use only at present</li>
        <li>No GPU acceleration</li>
        <li>Typically run with R1-7b model but occasionally 32b</li></ul>

</div>
<p class="clear"></p>

<div class="column">
  <h3 style="text-align: left">NAS Hardware:</h3>
    <p>Dell PowerEdge R730XD</p><ul>
        <li>Intel Xeon E5-2640 v4 10-core 2.4GHz</li>
        <li>256GB ECC DDR4</li>
        <li>12x 3.5" SAS3 front hotswap bays</li>
        <li>2x 2.5" SAS3 rear hotswap bays</li>
        <li>2x 750W 80+ Platinum power supplies</li>
        <li>2x 10GbE SFP+ 2x 1GbE mezzanine daughter card</li>
        <li>12x 20TB Western Digital Red HDDs</li>
        <li>2x 118GB Intel Optane P1600X m.2 NVMe SSDs</li></ul>
</div>
<div class="column">
  <h3 style="text-align: left">NAS Software and Configuration:</h3>
    <p>TrueNAS Core 13.0-U6.1</p><ul>
        <li>FreeBSD based</li>
        <li>ZFS pool</li>
        <li>Samba file sharing</li>
        <li>FreeBSD jail for lftp transfers</li></ul>
    <p>ZFS pool (Archives)</p><ul>
        <li>3x 4-drive vdevs each in RAIDZ1</li>
        <li>158TB usable space</li>
        <li>2x 118GB Optane SSDs for mirrored special metadata vdev</li>
        <li>Dedicated metadata storage extends HDD lifespans</li></ul>
</div>