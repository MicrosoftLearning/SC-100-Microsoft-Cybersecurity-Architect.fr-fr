# Global Secure Access

Après avoir configuré un serveur de surveillance, vous devez établir une mise en réseau sécurisée sur le serveur de fichiers à l’aide d’Accès global sécurisé (GSA). Vous souhaitez vous assurer que l’accès à ces machines est sécurisé jusqu’à ce que ces serveurs de fichiers puissent être migrés vers un stockage cloud sécurisé, en particulier si Tailwind Traders apporte des serveurs locaux dans l’infrastructure informatique de votre entreprise. Vous avez décidé de retravailler l’infrastructure VPN de Tailwind Traders pour permettre à vos employés d’accéder aux serveurs. 

Pour établir une mise en réseau sécurisée, vous allez commencer par créer un proxy Azure App et inscrire le client à Entra ID, avant de créer un connecteur. Après cela, vous allez configurer une stratégie d’accès et installer le client GSA. Enfin, vous allez tester la connexion GSA pour vérifier que tout fonctionne correctement.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez sécuriser l’accès à distance à votre environnement local.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Activer l’accès à distance sécurisé pour les serveurs locaux
- Intégrer à l’infrastructure existante
- Ne pas utiliser l’ancienne infrastructure de Tailwind Traders

Accès global sécurisé (GSA) s’intègre à l’infrastructure cloud actuelle de Contoso Ltd. et permet à vos employés de se connecter en toute sécurité à des serveurs locaux dans l’infrastructure locale de Tailwind Traders. Examinez le GSA et tenez compte des différences avec d’autres stratégies d’accès à distance aux services.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Activer l’accès à distance sécurisé pour les serveurs locaux| Accès global sécurisé Entra ID | Activer Accès global sécurisé  |
|Intégrer à l’infrastructure existante | Proxy d’application | Déployer le proxy d’application sur le serveur de fichiers de Contoso |

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : activer Accès global sécurisé

La première étape consiste à activer Accès global sécurisé dans votre locataire.

1. Connectez-vous à la machine virtuelle **LON-SC1** (point de terminaison client) en tant qu’**administrateur** local. Le mot de passe doit être fourni par votre fournisseur d’hébergement de labo.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **https://entra.microsoft.com** et connectez-vous au portail Entra en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
1. Dans la boîte de dialogue **Rester connecté ?**, cochez la case **Ne plus afficher**, puis sélectionnez **Non**.
1. Dans la boîte de dialogue **Enregistrer le mot de passe**, sélectionnez **Pas maintenant**.
1. Si une boîte de dialogue **Se connecter à Microsoft Edge** s’affiche, sélectionnez **Non merci**.
1. Si vous voyez une zone d’informations en haut à droite de l’écran qui indique **Gérer l’authentification multifacteur**, fermez-la en cliquant sur le **X**.
1. Dans le volet de navigation de gauche, développez **Accès global sécurisé** et sélectionnez **Tableau de bord**.
1. Sous **Activer Accès global sécurisé dans votre locataire**, sélectionnez **Activer**.

Vous avez activé Accès global sécurisé.

### Tâche 2 : activer TLS et installer le connecteur de réseau privé

Le connecteur de réseau privé est un agent léger installé sur un serveur Windows, dans votre environnement local, qui a accès aux ressources et applications backend et est utilisé pour faciliter la connexion au service Accès global sécurisé.  TLS 1.2 doit être activé sur le serveur Windows avant l’installation du connecteur du réseau privé.

1. Connectez-vous à la machine virtuelle du serveur **LON-SC2** avec le compte **Administrateur** local. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Lorsque vous vous connectez à la machine virtuelle, le gestionnaire de serveur s’ouvre.  Vous pouvez réduire cette fenêtre.
1. TLS 1.2 doit être activé avant l’installation du connecteur du réseau privé sur le serveur.  Il existe plusieurs façons de procéder. Pour cet exercice, vous allez copier les commandes pour définir les clés de registre dans un fichier, puis exécuter ce fichier.

    1. Ouvrez **Microsoft Edge**.
    1. Entrez l’URL **`https://learn.microsoft.com/en-us/entra/global-secure-access/how-to-configure-connectors`** dans votre navigateur puis appuyez sur la touche Entrée de votre clavier pour ouvrir la documentation du produit.
    1. Faites défiler la section **Exigences TLS (Transport Layer Security)** et, dans la zone de code fournie sous **Définir les clés de registre**, sélectionnez **Copier**
    1. Ouvrez le Bloc-notes dans la machine virtuelle. Dans le champ de recherche de la barre des tâches, tapez **`Notepad`**, puis sélectionnez **Bloc-notes** pour ouvrir l’application.
    1. Utilisez **Ctrl+V** pour coller le code dans le Bloc-notes.  Ne modifiez RIEN dans le code collé. La première ligne de code est requise.
    1. Dans le Bloc-notes, sélectionnez **Fichier**, puis **Enregistrer sous**. 
    1. Dans le champ **Enregistrer en tant que type**, sélectionnez **Tous les fichiers** dans la liste déroulante, puis, dans le champ **Nom de fichier**, entrez **`EnableTLS.reg`**, puis sélectionnez **Enregistrer**.  Il est important d’enregistrer le fichier avec l’extension .reg. Prenez note de l’emplacement d’enregistrement du document, puis fermez le Bloc-notes.
    1. Dans la barre des tâches, ouvrez **Explorateur de fichiers** et accédez au dossier dans lequel vous avez enregistré le fichier (l’emplacement par défaut est Ce PC > Documents).
    1. Double-cliquez sur le nom du fichier **Enable-TLS** pour l’exécuter.  Comme vous allez modifier le fichier de registre, il vous sera demandé **Voulez-vous vraiment continuer ?**  Sélectionnez **Oui**, puis **OK**.  
    1. Comme vous avez mis à jour le registre, vous devez redémarrer le serveur. Dans la barre des tâches de la machine virtuelle du serveur, sélectionnez l’**icône Windows**, puis **Marche/Arrêt**, puis **Redémarrer**, et enfin **Continuer**.
    1. Après le redémarrage, reconnectez-vous à la machine virtuelle du serveur, en tant qu’**administrateur** local.
    1. Réduisez ou fermez Gestionnaire de serveur.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **`https://entra.microsoft.com`** et connectez-vous au portail Entra en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
1. Ignorez les boîtes de dialogue, comme vous l’avez fait lors de la tâche précédente.
1. Dans le volet de navigation de gauche, développez **Accès global sécurisé**, développez **Se connecter** et sélectionnez **Connecteurs**.
1. En haut de la page Connecteurs de réseau privé, sélectionnez **Télécharger le service connecteur**.
1. Lisez les informations, puis sélectionnez **Accepter les conditions et télécharger**.
1. Dans la fenêtre des téléchargements située en haut à droite de la page, sélectionnez **Ouvrir le fichier** lorsque le téléchargement est terminé.  Si la fenêtre des téléchargements se ferme avant que vous ayez pu sélectionner Ouvrir un fichier, sélectionnez **Explorateur de fichiers** dans la barre des tâches, accédez au dossier **Téléchargements**, puis exécutez le fichier **MicrosoftEntraPrivateNetworkConnectorInstaller**.
1. Cochez la case à côté de **J’accepte les conditions générales de la licence**, puis sélectionnez **Installer**.
1. Pendant le processus d’installation, vous devez vous connecter avec le nom d’utilisateur et le mot de passe de l’administrateur MOD. L’installation peut prendre quelques minutes.
1. Une fois l’installation terminée, **fermez** la fenêtre d’installation et actualisez la page du navigateur.  Le connecteur devrait être affiché et actif.
1. Dans la barre de recherche Windows, dans la barre des tâches, entrez **`cmd`**, puis sélectionnez **Invite de commandes**. 
1. Dans la fenêtre Administrateur : invite de commandes, exécutez la commade **`ipconfig`**, notez l’adresse IP privée de votre serveur, puis fermez la fenêtre d’invite de commandes.

Vous avez correctement installé le connecteur de réseau privé sur votre serveur local.

### Tâche 3 : créer un dossier sur le serveur de fichiers

Dans cette tâche, vous allez créer un partage SMB sur le serveur de fichiers local accessible via GSA.

1. Vous devriez toujours vous trouver dans LON-SC2.
1. Dans la barre des tâches, ouvrez **Explorateur de fichiers**, accédez au lecteur C: et créez un dossier nommé **Partager**.
1. À l’aide du bouton droit de la souris, sélectionnez le dossier **Partager**, puis sélectionnez **Propriétés**.
1. Dans la fenêtre Propriétés du partage, sélectionnez l’onglet **Partage**.
1. Sélectionnez **Partager...**.
1. Dans la liste déroulante, sélectionnez **Tout le monde**, puis **Ajouter**.
1. Sélectionnez **Partager**.
1. Sélectionnez **Non, définir le réseau auquel je suis connecté comme réseau privé**.
1. Sélectionnez **Terminé**, puis **Fermez**.
1. Réduisez ou fermez l’Explorateur de fichiers.

Vous avez créé un dossier partagé sur le serveur. C’est à ce dossier et son contenu que vous accéderez via GSA.

### Tâche 4 : configurer Accès rapide et affecter l’utilisateur

L’Accès privé offre deux façons de configurer les ressources privées que vous souhaitez tunneliser via le service. Applications à accès rapide ou à accès global sécurisé. Pour cet exercice, vous allez utiliser l'accès rapide.

L’Accès rapide est le groupe principal de noms de domaine complets et d’adresses IP que vous souhaitez sécuriser. Lorsque vous configurez l’accès rapide, vous créez une application d’entreprise qui sert de conteneur pour les ressources privées que vous souhaitez sécuriser.

Pour permettre à vos utilisateurs d’accéder aux ressources du serveur de fichiers via le client GSA, vous devez activer l’accès rapide et l’affecter à vos utilisateurs de test.

1. Vous pouvez rester dans LON-SC2 pour cette étape.
1. Dans le volet de navigation de gauche, développez **Accès global sécurisé**, développez **Applications**, puis sélectionnez **Accès rapide**. Saisissez les informations suivantes :
    - Nom : **`SMB to ContosoFS`**
    - Groupe de connecteurs : **Par défaut**
1. Sélectionnez **Ajouter un segment d’application Accès rapide** et renseignez les informations suivantes :
    - Type de destination : **adresse IP**
    - Adresse IP : adresse IP privée de votre serveur que vous avez notée à l’étape **`192.168.2.100`**.
    - Ports : **`445`**
1. Sélectionnez **Appliquer**.
1. Cliquez sur **Enregistrer**. Une fois que le champ du segment de l’application affiche un état de réussite, actualisez la page du navigateur. Lorsque la page est actualisée, vous accédez à la page **Accès rapide | Propriétés d’accès au réseau**.
1. Dans le volet de gauche, sélectionnez **Utilisateurs et groupes**.
1. Sélectionner **Ajouter un utilisateur/groupe**.
1. Sélectionnez **Aucun sélectionné**.
1. Dans la zone de recherche, entrez **`MOD Administrator`**, puis sélectionnez-le dans les résultats de la recherche.
1. En bas de la page, cliquez sur **Sélectionner**, puis sélectionnez **Affecter**.

Vous avez activé l’accès rapide pour votre utilisateur de test.

### Tâche 5 : Entra ID de jointure d’appareil

Pour utiliser l’accès global sécurisé, vous devez joindre le point de terminaison client, la machine virtuelle LON-SC1, à Microsoft Entra ID. Sinon, le client GSA ne fonctionnera pas.

1. Revenez à la machine virtuelle **LON-SC1** (il s’agit de la machine virtuelle de votre point de terminaison client)
1. À l’aide du bouton droit de la souris, sélectionnez l’icône Windows dans la barre des tâches, puis sélectionnez **Paramètres**.
1. Sélectionnez **Comptes** dans le volet de navigation de gauche.
1. Sur la page Comptes, sélectionnez **Accès professionnel ou scolaire**.
1. Pour ajouter un compte professionnel ou scolaire, sélectionnez **Se connecter**.
1. En bas de la fenêtre, sélectionnez **Joindre l’appareil à Microsoft Entra ID**.
1. Connectez-vous avec les informations d’identification d’**administrateur MOD** fournies par le fournisseur de labo.
1. Dans la fenêtre **Vérifier qu’il s’agit de votre organisation**, passez en revue les informations, puis sélectionnez **Joindre**.
1. Passez en revue les informations de la fenêtre **Vous êtes prêt**, puis sélectionnez **Terminé**.
1. Maintenant que votre appareil a été joint à Entra ID avec votre compte d’administrateur MOD, vous devez vous connecter à l’aide de ce compte.
    1. Dans la barre des tâches, sélectionnez l’icône **Windows**, puis cliquez sur **Admin** et sélectionnez **Changer d’utilisateur**.
    1. En bas à gauche de la fenêtre, sélectionnez **Autre utilisateur**, puis connectez-vous avec votre compte d’administrateur MOD.
    1. La configuration du compte prendra quelques minutes. Vous verrez alors la fenêtre **Plus d’informations sont nécessaires** s’afficher. Cela lance le processus de configuration de l’authentification multifacteur.  Suivez les instructions de configuration.

Une fois que votre point de terminaison est joint à Entra ID, vous pourrez configurer le client GSA utilisé pour vous connecter à toutes les ressources que vous protégez avec l’accès global sécurisé.

### Tâche 6 : Activer le profil de transfert de trafic et télécharger le client de bureau GSA

Pour activer l’accès aux ressources privées ou aux applications dans votre environnement local, vous devez activer le profil de transfert de trafic pour l’accès privé et affecter des utilisateurs.

Vous devez également télécharger et installer le client de bureau de l'accès global sécurisé.  

Le trafic Accès privé peut être transféré au service avec une connexion via le client de bureau Accès global sécurisé.

1. Vous devez toujours être sur la machine virtuelle **LON-SC1**, à laquelle vous êtes connecté avec votre compte d’administrateur MOD.
1. Ouvrez **Microsoft Edge**. Vous serez invité à configurer Microsoft Edge.
1. Dans Microsoft Edge, accédez à **`https://entra.microsoft.com`**.
1. Dans le volet de navigation de gauche, développez **Accès global sécurisé**, développez **Se connecter** et sélectionnez **Transfert du trafic**.  Vous devrez peut-être développer le volet de navigation de gauche en sélectionnant **>>** pour afficher les options.
1. Sélectionnez le curseur en regard de **Profil d’accès privé**, puis sélectionnez **OK**.
1. Maintenant que vous avez activé le profil d’accès privé, vous devez affecter des utilisateurs.
    1. Dans la carte Profil d’accès privé, sous **Affectations des utilisateurs et des groupes**, sélectionnez **Affichage**.
    1. Sélectionnez **0 utilisateurs, 0 groupes affectés**
    1. Sélectionner **Ajouter un utilisateur/groupe**.
    1. Sélectionnez **Aucun sélectionné**.
    1. Dans la barre de recherche, entrez **`MOD Administrator`**, sélectionnez **Administrateur MOD**, cliquez sur **Sélectionner**, puis sélectionnez **Affecter**.
1. Dans le volet de navigation de gauche, sous **Se connecter**, choisissez **Téléchargement du client**.
1. Sous Windows 10/11, sélectionnez **Télécharger le client**.
1. Dans la fenêtre Téléchargements, sélectionnez **Ouvrir le fichier**. Si la fenêtre de téléchargement est fermée avant de pouvoir sélectionner Ouvrir un fichier, sélectionnez **Explorateur de fichiers** dans la barre des tâches, accédez au dossier **Téléchargements**, puis exécutez le fichier **GlobalSecureAccessClient**.
1. Sélectionnez **J’accepte les conditions générales du contrat de licence**, puis sélectionnez **Installer**. Dans la fenêtre Contrôle de compte d’utilisateur qui s’affiche, sélectionnez **Oui**.
1. Une fois l’installation terminée, **fermez** la fenêtre.
1. Dans la barre des tâches, sélectionnez la flèche vers le haut pour afficher les icônes masquées.  Ici, vous verrez l’icône du client Accès global sécurisé. S’il n’a pas de coche verte, cliquez avec le bouton droit sur l’icône et sélectionnez **Activer**. Plusieurs minutes peuvent s’écouler avant qu’une coche verte ne s’affiche pour indiquer que la connexion est établie.
1. Dans la barre des tâches, sélectionnez **Explorateur de fichiers** et accédez à **Ce PC**. Sélectionnez les points de suspension (**...**) et sélectionnez **Mapper le lecteur réseau**.
1. Dans le champ Dossier, entrez `\\192.168.2.100\Share`. Utilisez l’adresse IP que vous avez notée précédemment ET sélectionnez **Se connecter à l’aide de différentes informations**.
1. Sélectionnez **Terminer**.
1. Pour mapper le lecteur réseau, utilisez les informations d’identification du compte d’administrateur local sur LON-SC2.  
    1. Champ E-mail : **`Administrator`** (cela peut varier selon l’hébergeur de labo).
    1. Champ Mot de passe : **`Pa55w.rd`** (cela peut varier selon l’hébergeur de labo).
    
    >[!NOTE] Il est clair que l’utilisation du compte d’administrateur local n'est pas un scénario habituel. Il est utilisé dans cet exercice en raison de l’environnement local simplifié. Dans un scénario plus réaliste, avec un environnement sur site plus impliqué, l’utilisateur accèderait aux ressources privées avec son compte Entra ID.

1. Avant de passer au labo suivant, il est recommandé de changer d’utilisateur pour une taille d’écran optimale.
    1. Dans la barre des tâches, sélectionnez l’icône **Windows**, sélectionnez **Administrateur MOD**, puis sélectionnez **Changer d’utilisateur**.
    1. En bas à gauche de la fenêtre, sélectionnez **Admin**, puis connectez-vous avec votre compte Administrateur local.

Vous avez établi une connexion au serveur de fichiers à l’aide d’Accès global sécurisé.
