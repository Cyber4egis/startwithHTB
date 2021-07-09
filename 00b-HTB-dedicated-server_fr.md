# Comment se connecter à un serveur pour un évènement Hack The Box
Ce document décrit comment se connecté au serveur Hack The Box dédié à l'atelier *Tes Premiers Pas avec Hack The Box* par Cristina Solana pour Cyber Aegis. 

Seules les participantes dont le nom d'usager aura été ajouté au serveur dédié pourront y accéder. Pour avoir accès au serveur le jour de l'évènement, veuillez vous assurez d'en avoir fait la requêtes aux organisatrices. 

## Étape 1 – Changer l'interface de Hack The Box
Si tu utilises la nouvelle interface de Hack The Box, tu devras utiliser l'interface classique *Classic HTB*  pour la durée de cet atelier.
Cela se fait en cliquant sur ton nom d'usager et en sélectionnant *Classic HTB*.

![image1](/assets_/1.png)

## Étape 2 – Générer et télécharger une "Connection Pack"
Dans le menu à gauche, sélectionne *Access*.

 ![image2](/assets_/2.png)
 
Sous la section *Tickets*, sélectionne le bouton *Switch* sur le ticket *Dedicated* et selectionne le serveur *US Dedicated 12*.

 ![image3](/assets_/3.png)
 
Quand le changement d'interface est complété, sélectionne le bouton *Refresh*.

 ![image4](/assets_//4.png)

Tu devrais à présent void, le nom du serveur auquel tu es connectée.

 ![image5](/assets_/5.png)

 Clique ensuite sur le bouton *Connection Pack*.

 ![image6](/assets_/6.png)


## Étape 3 - Connection au serveur dédié

Execute la commande suivante:

```
sudo openvpn <nomdusager>.ovpn
```

Tu devrais voir ce résultat:

 ![image8](/assets_/8.png)
 
 
 ## Étape 4 - Teste la connection
 
 D'abord, confirme que l'on t'a assigné une adresse IP en exécutant la commande suivante:
 
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
 
 Dans le menu de gauche, clique sur *Dedicated Labs* > selectionne *US Dedicated 12*. Tu verras une liste the machines disponibles et leur adresse IP correspondante.
 
  ![image9](/assets_/9.png)
  
  Ping une des adresses IP pour tester ta connection.
  
```
root@kali:~# ping 10.10.10.85
PING 10.10.10.85 (10.10.10.85) 56(84) bytes of data.
64 bytes from 10.10.10.85: icmp_seq=1 ttl=63 time=45.5 ms
64 bytes from 10.10.10.85: icmp_seq=2 ttl=63 time=37.6 ms
64 bytes from 10.10.10.85: icmp_seq=3 ttl=63 time=34.2 ms
64 bytes from 10.10.10.85: icmp_seq=4 ttl=63 time=51.0 ms
```

Ces instructions ont été écrites par [Rana Khalil](https://github.com/rkhal101) et ont été adaptées pour cet atelier.
