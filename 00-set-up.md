# Set-Up

1. [Download VirtualBox for your operating system and install it.](https://www.virtualbox.org/)
2. [Dowload the lastest Kali Linux Virtualbox image](https://www.kali.org/get-kali/#kali-virtual-machines). Make sure to download the image for VirtualBox and not the one for VMware.
3. Open VirtualBox and click on « File » > « Import Appliance… »
4. Click on the yellow folder and import your Kali image (.ova file)
5. Once the image is imported, you can launch it by clicking on Start (green arrow) 
6. Log into Kali. Username: kali. Password: kali.
7. Open a browser within Kali and log into hackthebox.eu.
8. At the top right, click on CONNECT TO HTB, Starting Point and OpenVPN.
9. Select the VPN server closest to you and click on Download VPN. The file name will be *starting_point_yourusername.ovpn*
10. Open a termninal within Kali, locate the full path to your VPN configuration file and run the following command: `sudo openvpn starting_point_htbusername.ovpn`.
11. Return to hackthebox.eu. On the left-side menu, select Labs then Starting Point. Click on the machine named Archetype and then on Join Machine. 
12. Take note of the machine's ip address.
13. Return to your terminal and ping the ip address you noted.
