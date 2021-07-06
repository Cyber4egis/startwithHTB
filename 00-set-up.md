# Setup Instructions

1. [Download VirtualBox for your operating system and install it.](https://www.virtualbox.org/)

![VirtualBox](/assets_/downloadVB.png)

2. [Download the lastest Kali Linux VirtualBox image](https://www.kali.org/get-kali/#kali-virtual-machines). Make sure to download the image for VirtualBox and not the one for VMware.
3. Open VirtualBox and click on « File » > « Import Appliance… »

![Import1](/assets_/importvm.png)

4. Click on the yellow folder and import your Kali image (.ova file)

![Import2](/assets_/importvm2.PNG)

5. Once the image is imported, you can launch it by clicking on Start (green arrow) 

![VMStart](/assets_/vm_start.png)

6. Log into Kali. *Username: kali. Password: kali.*

![Login](/assets_/kalikali.png)

7. Open a terminal within Kali and install [feroxbuster](https://github.com/epi052/feroxbuster) by running the following command: `sudo apt install feroxbuster`

![Feroxbuster](/assets_/feroxbuster.png)

8. Your Kali VM is ready for the workshop!

## Test Your VPN Connection to Hack The Box

The following instructions are to verify that you can successfully connect to Hack The Box through OpenVPN with your Kali Linux VM. The day before the workshop, we will send you updated instructions to connect to our dedicated server.

1. Open a browser within Kali and log into [hackthebox.eu](https://www.hackthebox.eu/).
2. At the top right, click on *CONNECT TO HTB*, then click on *Machines* and then click on *OpenVPN*.

![Connect](/assets_/connectothtb.PNG)

![Machines](/assets_/machines.PNG)

![OpenVPN](/assets_/openvpn.PNG)

3. Select the VPN server closest to you and click on *Download VPN*. It may take a few seconds before the Download VPN button is enabled. The file name will be *username.ovpn*

![OpenVPN](/assets_/downloadVPN.PNG)

4. Open a terminal within Kali, locate the full path to your VPN configuration file (.ovpn file) and run the following command: `sudo openvpn username.ovpn`.
5. Return to [hackthebox.eu](https://www.hackthebox.eu/). On the left-side menu, select *Labs* then select *Machines*. 

![Labs](/assets_/Labs_machines.PNG)


6. Search for an active machine called **Love** and click on its name then click on **Join Machine**. 

![SearchLove](/assets_/search_love.PNG)

![Join](/assets_/join.PNG)

7. Take note of the ip address for *Love*.

![Love](/assets_/love_ip.PNG)

8. Return to your terminal and open a new tab (Ctrl+Shift+T), then in the new terminal tab ping the ip address you noted. If you can ping the machine successfully, your VPN connection to Hack The Box works.
