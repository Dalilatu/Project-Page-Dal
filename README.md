<h1>Home Lab Setup</h1>

<h2>Description</h2>
This home lab simulates a small enterprise network designed for hands-on penetration testing. It includes an attacker machine, segmented networks, and an Active Directory environment to practice real-world attack scenarios and defensive analysis.
<br />


<h2>Utilities Used</h2>

- <b>pfSense</b>
- <b>Metasploitable</b>
- <b>Windows 11</b>
- <b>Windows Server</b>
- <b>Kali Linux</b>


<h2>Environments Used </h2>

- <b>Virtual Box</b>

<h2>Program walk-through:</h2>

<h3>Lab Installation Tools</h3>

| Tool Name | Why It Was Used | Download Link |
|-----------|---------------------------|---------------|
| VirtualBox | Used to create and manage virtual machines for the lab environment. | [Download](https://www.virtualbox.org/) |
| Kali Linux | Offensive security testing and penetration testing distribution. Will be used for our attacks| [Download](https://www.kali.org/get-kali/) |
| Metasploit | Exploitation framework used for vulnerability testing. | [Download](https://www.metasploit.com/) |
| pfSense | Firewall and router used to simulate network segmentation and traffic control in the lab. | [Download](https://www.wireshark.org/) |
| Windows 11 Enterprise | Will be used as our client machine | [Download](https://www.microsoft.com/en-us/evalcenter/download-windows-11-enterprise) |
| Windows Server | The server that'll be used for the Domain Controller | [Download](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2025) |


<h3>Lab Diagram</h3>

<p align="center">
<img src="https://github.com/Dalilatu/Project-Page-Dal/blob/main/Home%20lab%20Setup%20diagram.drawio.png?raw=true" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h3>Important Configuration</h3>

<!-- 
THIS SECTION EXPLAINS THE SETTING CONFIGURATION DONE ON VIRTUAL BOX FOR PFSENSE
--!>

<strong>1. PfSense Setting Configurations</strong>

<p align="center">
Go to settings: <br />
<br />
<img alt="image" src="https://github.com/user-attachments/assets/58ae9f74-d194-48fb-a30a-7f38f9cb9063" height="80%" width="80%"/>
</p>
<br />
<br />

<p align="center">
Configure System: <br />
<br />
<img src="https://github.com/user-attachments/assets/74692b6d-d801-4e01-9e2a-bf129ee10a30" height="80%" width="80%"/><br />
Hard Disk and Optical Drive must be selected and Hard Disk should be at the top. This is very important else pfSense will not start appropiately.
</p>
<br />
<br />

<p align="center">
Configure Network (Adapter 1): <br />
<br />
<img alt="image" src="https://github.com/user-attachments/assets/cf3bfbaa-4751-4501-a585-5a81b5361289" height="80%" width="80%"/><br />
 This is set to Bridged Adapter to enable access to the router.
</p>
<br />
<br />

<p align="center">
Configure Network (Adapter 2): <br />
<br />
<img src="https://github.com/user-attachments/assets/734125c1-b16e-43d2-b4da-809ec517623d" height="80%" width="80%"/><br />
 Set to Internal Network LAN 0 to be in thesame network as our Active Directory.
</p>
<br />
<br />

<p align="center">
Configure Network (Adapter 3): <br />
<br />
 <img src="https://github.com/user-attachments/assets/a14ef138-bdce-44ef-8ba5-30d431462145" height="80%" width="80%"/><br />
 Set to Internal Network LAN 1 to be in thesame network as our Attacking Machine.
</p>
<br />
<br />

<p align="center">
Disable USB: <br />
<br />
 <img src="https://github.com/user-attachments/assets/adbfd96e-cdc2-49bb-abd5-84e944fe54c5"  height="80%" width="80%"/><br />
</p>
<br />
<br />

Once pfSense is successfully installed, we can now go ahead and install other tools like Windows 11, Kali, Metasploitable and Windows Server.
<br />
<br />

<!-- CONFIGURING PFSENSE -->
<h3>pfSense Configuration 2: Firewall Configuration</h3>
<br/>

<h3>pfSense Configuration Guide</h3>

With <strong>pfSense</strong> and <strong>Windows 11</strong> running, access the pfSense web interface via: <br/>
<strong>https://pfsense_ip_address</strong><br/>
<br/>

This allows us to configure and manage the network interfaces.<br/>
<br/>

<h4>Configuration Steps Completed</h4><br/>

1️⃣ <strong>Services > DNS Resolver</strong><br/>

- Enable:<br/>
  - ✅ Register DHCP Leases in the DNS Resolver.<br/>
  - ✅ Register DHCP Static Mappings in the DNS Resolver.<br/>
<br/>
<strong>Services > DNS Resolver > Advanced Settings</strong><br/>

- Enable:<br/>
  - ✅ Prefetch Support<br/>
  - ✅ Prefetch DNS Key Support<br/>

<br/>
2️⃣ <strong>System > Advanced > Network</strong><br/>

- Enable:<br/>
  - ✅ Hardware Checksum Offloading<br/>

<br/>
3️⃣ <strong>Status > DHCP Leases</strong><br/>

- This section allows you to:<br/>
  - View active DHCP leases<br/>
  - Identify connected devices<br/>
  - Modify the Windows 11 IP address if necessary.
<br/>
<br/>
4️⃣ <strong>Services > DHCP Server</strong><br/>

Under <strong>Server Options</strong>:<br/>

- Add the following DNS servers:<br/>
  - `8.8.8.8`<br/>
  - `1.1.1.1`<br/>
<br/>
⚠️ Ensure this configuration is applied to both:<br/>
- <strong>ECORP</strong><br/>
- <strong>ATTACKLAN</strong><br/>
<br/>
(Select the appropriate interface tab before making changes.)<br/>
<br/>
<strong>Creating an Alias</strong><br/>
<br/>
To create a firewall alias:<br/>

1. Navigate to <strong>Firewall > Aliases</strong><br/>
2. Click <strong>Add</strong><br/>
3. Define:<br/>
   - Name<br/>
   - Description<br>
   - Type (Host, Network, Port, etc.)<br/>
4. Save and Apply changes<br/>
<br/>
Aliases help simplify firewall rule management and improve readability.<br/>
<br/>


<!--CREATING FIREWALL RULES-->


<strong>Creating Firewall Rules</strong><br/>


We configured firewall rules to:<br/>

Allow traffic between:<br/>
  - Active Directory and other devices within the same network<br/>
  - Active Directory and the ATTACKLAN<br/>
  - Active Directory and non-private (internet) networks<br/>
<br/>
Configure ATTACKLAN rules to:<br/>
  - Allow traffic to ECORP<br/>
  - Allow outbound internet access<br/>
<br/>
<br/>
<strong># Firewall Rules – Screenshots</strong><br/>

<strong>ECORP Firewall Rules</strong></br>
<p align="center">
ECORP firewall rules:<br/>

<img width="981" height="672" alt="image" src="https://github.com/user-attachments/assets/4ef2c8cc-9600-43c8-97da-79f8a310b8be"/><br/>

</p>

<strong>ATTACKLAN Firewall Rules</strong><br/>
<p align="center">
ATTACKLAN firewall rules:<br/>

<img width="947" height="510" alt="image" src="https://github.com/user-attachments/assets/85cbab3c-9606-416d-abdb-f85f636fc669" />
<br />

</p>
<br/>










<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
