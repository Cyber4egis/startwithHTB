# Set-Up Instructions

1. [Download VirtualBox for your operating system and install it.](https://www.virtualbox.org/)

![VirtualBox](/assets_/downloadVB.png)

2. [Dowload the lastest Kali Linux Virtualbox image](https://www.kali.org/get-kali/#kali-virtual-machines). Make sure to download the image for VirtualBox and not the one for VMware.
3. Open VirtualBox and click on « File » > « Import Appliance… »

![Import1](/assets_/importvm.png)

5. Click on the yellow folder and import your Kali image (.ova file)

![Import2](/assets_/importvm2.PNG)

7. Once the image is imported, you can launch it by clicking on Start (green arrow) 

![VMStart](/assets_/vm_start.png)

8. Log into Kali. *Username: kali. Password: kali.*

![Login](/assets_/kalikali.png)

10. Open a terminal within Kali and install feroxbuster by running the following command: `sudo apt install feroxbuster`
11. Your Kali VM is ready!

## Test Your VPN Connection to Hack The Box
1. Open a browser within Kali and log into [hackthebox.eu](https://www.hackthebox.eu/).
2. At the top right, click on *CONNECT TO HTB*, then click on *Machines* and then click on *OpenVPN*.
3. Select the VPN server closest to you and click on *Download VPN*. It may take a few seconds before the Download VPN button is enabled. The file name will be *username.ovpn*
4. Open a termninal within Kali, locate the full path to your VPN configuration file (.ovpn file) and run the following command: `sudo openvpn username.ovpn`.
5. Return to [hackthebox.eu](https://www.hackthebox.eu/). On the left-side menu, select *Labs* then select *Machines*. 
6. Search for an active machine called **Love** and click on its name then click on **Join Machine**. 
7. Take note of the ip address for *Love*.
8. Return to your terminal and ping the ip address you noted. If you can ping the machine successfully, your VPN connection to Hack The Box works.
