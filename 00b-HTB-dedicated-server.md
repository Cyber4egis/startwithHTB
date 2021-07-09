# How to Connect to the Dedicated Server
This document describes how to connect to the Hack The Box dedicated server for the Cyber Aegis *Getting Started with Hack The Box Workshop* by Cristina Solana. 

Note that only participants who were added to the dedicated server will have access to it. If you attend the workshop and need access to the server, make sure that you ask one of the organizers.

## Step 1 – Switch to Classic HTB UI
If you are using the *New UI*, you need to switch back to the *Classic HTB* UI for the duration of this workshop.
This can be done by clicking on your username > select *Classic HTB*.

![image1](/assets_/1.png)

## Step 2 – Generate and Download Connection Path
On the menu on the left, click on *Access*.

 ![image2](/assets_/2.png)
 
Under the *Tickets* section, click on the *Switch* button on the Dedicated ticket and select the dedicated server *US Dedicated 12*.

 ![image3](/assets_/3.png)
 
When the switch is completed, click on the *Refresh* button.

 ![image4](/assets_//4.png)

Once refreshed, you should see the name of the server you connected to.

 ![image5](/assets_/5.png)

 Then click on the *Connection Pack* button.

 ![image6](/assets_/6.png)


## Step 3 - Connect to the Dedicated Server

Run the following command.

```
sudo openvpn <username>.ovpn
```

This should generate the following output.

 ![image8](/assets_/OpenVPN_academy.PNG.png)
 
 
 ## Step 4 - Test the Connection
 
 First, confirm that you've been given an IP address.
 
 ```
 root@kali:~# ifconfig      
 ....
 tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.10.14.2  netmask 255.255.254.0  destination 10.10.14.2
        inet6 dead:beef:2::1000  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::ce00:662a:f97:2c8f  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen 100  (UNSPEC)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1  bytes 48 (48.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
 ```
 
 On the menu on the left, click on *Dedicated Labs* > select *US Dedicated 12*. There you'll see the list of available boxes on the dedicated server and the associated IP addresses.
 
  ![image9](/assets_/9.png)
  
  Ping one of the IPs to test the connection.
  
```
root@kali:~# ping 10.10.10.85
PING 10.10.10.85 (10.10.10.85) 56(84) bytes of data.
64 bytes from 10.10.10.85: icmp_seq=1 ttl=63 time=45.5 ms
64 bytes from 10.10.10.85: icmp_seq=2 ttl=63 time=37.6 ms
64 bytes from 10.10.10.85: icmp_seq=3 ttl=63 time=34.2 ms
64 bytes from 10.10.10.85: icmp_seq=4 ttl=63 time=51.0 ms
```

This tutorial was written by [Rana Khalil](https://github.com/rkhal101) and adapted for this workshop.
