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
| Windows Server | The server that'll be used for the Domain Controller | [Download](link) |


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




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
