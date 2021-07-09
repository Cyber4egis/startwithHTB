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

Tu devrais à présent voir, le nom du serveur auquel tu es connectée.

 ![image5](/assets_/5.png)

 Clique ensuite sur le bouton *Connection Pack*.

 ![image6](/assets_/6.png)


## Étape 3 - Connection au serveur dédié

Execute la commande suivante:

```
sudo openvpn <nomdusager>.ovpn
```

Tu devrais voir ce résultat:

![OpenVPN](/assets_/OpenVPN_academy.PNG)
 
 
 ## Étape 4 - Teste la connection
 
 Si tu tapes `ifconfig` dans une autre fenêtre du terminal, tu verras un adapteur *tun* si tu es bien connectée au VPN. 
 
 ![OpenVPN](/assets_/ifconfig.PNG)
 
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
