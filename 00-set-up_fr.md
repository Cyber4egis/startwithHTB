# Instructions

1. [Télécharge VirtualBox pour ton système d'exploitation et installe-le.](https://www.virtualbox.org/)

![VirtualBox](/assets_/downloadVB.png)

2. [Télécharge la dernière version de l'image de Kali Linux](https://www.kali.org/get-kali/#kali-virtual-machines). Assure-toi de télécharger l'image faite pour VirtualBox et non celle faite pour VMware.

![Import1](/assets_/importvm.png)

4. Clique sur le répertoire jaune et importe l'image de Kali que tu viens de télécharger (fichier .ova)

![Import2](/assets_/importvm2.PNG)

5. Une fois l'image importée, tu peux la lancer en cliquant sur Start (flèche verte) 

![VMStart](/assets_/vm_start.png)

Il est possible que tu rencontres ce message d'erreur en démarrant ta machine virtuelle Kali Linux. 

![Erreur](/assets_/error1.png)

Tu peux rémédier la situation en désactivant le support pour USB 2.0 dans la configuration de ta MV **OU** en installant la version la plus récente de [Oracle VM VirtualBox Extension Pack](https://www.virtualbox.org/wiki/Downloads).

![ExtensionPack](/assets_/vbextensionpack.png)

6. Authentifie-toi à Kali. *Nom d'usager: kali. Mot de passe: kali.*

![Login](/assets_/kalikali.png)

7. Dans Kali, ouvre une fenêtre de terminal et installe [*feroxbuster*](https://github.com/epi052/feroxbuster) avec la commande suivante: `sudo apt update && sudo apt install -y feroxbuster`

![Feroxbuster](/assets_/feroxbuster.png)

8. Ta machine virtuelle Kali est prête! 👍

## Teste ta connection VPN avec Hack The Box

Les instructions suivantes servent à vérifier que ta machine virtuelle Kali Linux est capable de se connecter à Hack The Box avec OpenVPN. Le jour qui précédera l'atelier, nous t'enverrons des instructions mises à jour afin que tu te connectes au serveur Hack The Box dédié à Cyber Aegis.

1. Dans Kali, ouvre un navigateur web et connecte-toi à [hackthebox.eu](https://www.hackthebox.eu/) avec ton nom d'usager.
2. En haut à droite, clique sur *CONNECT TO HTB*, ensuite clique sur *Machines* et finalement clique sur *OpenVPN*.

![Connect](/assets_/connectothtb.PNG)

![Machines](/assets_/machines.PNG)

![OpenVPN](/assets_/openvpn.PNG)

3. Sélectionne le serveur VPN le plus proche de toi et clique sur *Download VPN*. Cela peut prendre quelques secondes avant que le bouton *Download VPN* s'active. Le fichier portera le nom de ton nom d'usager avec l'extenstion .ovpn.

![DownloadVPN](/assets_/downloadVPN.PNG)

4. Ouvre une fenêtre de terminal dans Kali, et execute la commande suivante: `sudo openvpn username.ovpn`. Assure-toi d'être dans le répertoire où se situe ton fichier de configuration .ovpn
5. Retourne sur le site de [hackthebox.eu](https://www.hackthebox.eu/). Dans le menu de gauche, selectionne *Labs* et selectionne ensuite *Machines*. 

![Labs](/assets_/Labs_machines.PNG)


6. Amorce une recherche pour trouver la machine active nommée *Love*, clique sur le nom de la machine puis sur  *Join Machine*. 

![SearchLove](/assets_/search_love.PNG)

![Join](/assets_/join.PNG)

7. Prends en note l'adresse ip de la machine *Love*.

![Love](/assets_/love_ip.PNG)

8. Retourne vers ton terminal dans Kali et ouvre un autre onglet (Ctrl+Shift+T). Dans ce nouvel onglet, ping l'adresse ip que tu as prise en note. Si ta commande ping s'execute avec succèes, ta connection VPN vers Hack The Box fonctionne correctement. 👍
