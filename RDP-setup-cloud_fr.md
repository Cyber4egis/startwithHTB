# Remote Desktop pour les instances dans le Cloud

Selon ton système d'exploitation, choisis les instructions qui te conviennent:
1. [Remote Desktop pour Windows](#Remote-Desktop-pour-Windows)
2. [Remote Desktop pour Mac](#Remote-Desktop-pour-Mac)
3. [Remote Desktop pour Linux](#Remote-Desktop-pour-Linux)

## Remote Desktop pour Windows

1. Le client Remote Desktop Connection vient installé sure Windows. Si vous utilisez un machine Windows, aucun logiciel additionnelle n'a à être installé.

2. Téléchargez le fichier *.rdp que l'on vous distribuera durant l'atelier. 

3. Double-cliquez sur le fichier et une fenêtre de Remote Desktop Connection s'ouvrira.

![RDC](/assets_/RDC.png)

4. Cliquez sur **Connect**.
 
5. Entrez les informations d'identification que l'on vous aura fourni durant l'atelier. Utilisez l'option **More choices** si vous devez changer le _nom d'utilisateur_.

![credentials](/assets_/credentials.png)

6. Cliquez sur **OK**.

7. Vous verrez l'avertissement suivant : "_The identity of the remote computer cannot be verified. Do you want to connect anyway?_" Cliquez sur **Yes**.

![sayyes](/assets_/sayyes.png)

## Remote Desktop pour Mac
1. Installez Microsoft Remote Desktop à partir de l'App store.

2. Téléchargez le fichier RDP qui vous a été envoyé. Selectionnez __ouvrir avec__ et ensuite __Microsoft Remote Desktop__ à partir du menu déroulant orsque vous y êtes invité par l'action de téléchargement:

    ![save_as](/assets_/save_as.png)

    Si vous ne sélectionnez pas __ouvrir avec "Microsoft Remote Desktop"_ lorsque vous téléchargez, vous pouvez cliquez-droit sure le fichier et sélectionner __Ouvrir avec__ -> Microsoft Remote Desktop.

3. Dans la fenêtre de connexion, entrez le mot de passe qui vous a été donné et cliquez sur _-Continuer__.

![passwd_mac](/assets_/passwd_mac.png)

4. Vérification CERT: après l'étape 3, vous devriez voir uen fenêtre pop up comme suit Sélectionnez __Continuer__ et votre session commencera.

    ![cert_mac2](/assets_/cert_mac2.png)
    
## Remote Desktop pour Linux
1. Installez __Itopa__ flatpak. Le plus simple est de le faire à partir du gestionnaire de logiciel. 

2. Téléchargez le fichier RDP qui vous a été envoyé. Sélectionnez __Ouvrir avec itopia__ lorsque la fenêtre s'affiche.
![openwith](/assets_/openwith.png)

    Si vous ne sélectionnez pas _"ouvrir avec itopia"_, vous pouvez ajouter l'information manuellement dans itopia comme suit: 
![copy_info_](/assets_/copy_info_.png) 
et cliquez __Connect__.

3. Verification Cert: Après l'étape 2, vous devriez voir une fenêtre pop up comme suit. Sélectionnez __Ok__.
![certs](/assets_/certs.png)

4. Vous devriez voir la fenêtre de connexion, entrez le mot de passe qui vous a été fourni, cliquez -_OK__ et votre session commencera.
![passwd](/assets_/passwd.png)
