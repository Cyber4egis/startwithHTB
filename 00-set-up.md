# Set-Up

1. [Download VirtualBox for your operating system and install it.](https://www.virtualbox.org/)
2. [Dowload the lastest Kali Linux Virtualbox image](https://www.kali.org/get-kali/#kali-virtual-machines). Make sure to take the image for VirtualBox and not the one for VMware.
3. Open VirtualBox and click on « File » > « Import Appliance… »
4. Click on the yellow folder and navigate to the image of Kali (.ova file) you downloaded, select it and click on Import
5. Once the image is imported, you can launch the image by clicking on Start (green arrow) 
6. Log into Kali. Username: kali. Password: kali.
7. OpenVPN, should already be installed. If not, open the termninal and install it by running the following command: `sudo apt install openvpn`
8. Locate the full path to your VPN configuration file, normally in your Downloads folder.
9. Use your OpenVPN file with the following command: `sudo openvpn /path-to-file/file-name.ovpn`
