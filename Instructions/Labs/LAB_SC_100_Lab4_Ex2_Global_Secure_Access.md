# Labo 4 - Exercice 2 - Accès global sécurisé

Après avoir configuré le serveur de surveillance, vous devez établir une mise en réseau sécurisée sur le serveur de fichiers à l’aide d’Accès global sécurisé (GSA). Vous souhaitez vous assurer que l’accès à ces machines est sécurisé jusqu’à ce que ces serveurs de fichiers puissent être migrés vers un stockage cloud sécurisé, en particulier si Tailwind Traders apporte des serveurs locaux dans l’infrastructure informatique de votre entreprise. Vous avez décidé de retravailler l’infrastructure VPN de Tailwind Traders pour permettre à vos employés d’accéder aux serveurs. 

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
<!--BITE AUSFÜLLEN-->
|Exigence|Solution|Plan d’action|
|----|----|----|
|Activer l’accès à distance sécurisé pour les serveurs locaux| Accès global sécurisé Entra ID | Activer Accès global sécurisé  |
|Intégrer à l’infrastructure existante | Proxy d’application | Déployer le proxy d’application sur le serveur de fichiers de Contoso |

## Partie 2 : implémenter la solution (facultatif)

## Tâche 1 : activer Accès global sécurisé

La première étape consiste à activer Accès global sécurisé dans votre locataire. Cela vous permet d’utiliser un proxy Azure App pour fournir un accès sécurisé aux ressources locales.

1. Connectez-vous à la **machine virtuelle Client 1** (LON-SC1) avec le compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **https://entra.microsoft.com** et connectez-vous au portail Entra en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
3. Il vous sera demandé de configurer l’authentification multifacteur ; suivez les instructions.
4. Dans la boîte de dialogue Rester connecté ?, cochez la case Ne plus afficher, puis sélectionnez **Non**.
5. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant Jamais, pour ne pas enregistrer les informations d’identification des administrateurs généraux par défaut dans votre navigateur.
6. Dans le volet de navigation de gauche, développez **Accès global sécurisé** et sélectionnez **Tableau de bord**.
7. Sous **Activer Accès global sécurisé dans votre locataire**, sélectionnez **Activer**.

Vous avez activé Accès global sécurisé.

## Tâche 2 : déployer le proxy d’application

Accès global sécurisé est basé sur le proxy d’application qui vous permet de créer un point de terminaison cloud sécurisé pour vos ressources locales. Dans ce cas, vous allez autoriser le serveur de test que vous avez configuré précédemment à communiquer via l’infrastructure proxy.

1. Connectez-vous à la **machine virtuelle Server 1** (LON-SC2) avec le compte **lon-sc1\admin**. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **https://entra.microsoft.com** et connectez-vous au portail Entra en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
3. Sous **Accès global sécurisé **, dans le volet de navigation de gauche, développez **Se connecter** et sélectionnez **Connecteurs**.
4. Sélectionnez **Télécharger le service de connecteur**.
5.  Sélectionnez **Accepter les conditions et télécharger**.
6.  Installez le **connecteur du proxy d’application Microsoft Azure Active Directory**.
7.  Pendant le processus d’installation, vous devez vous connecter avec le nom d’utilisateur et le mot de passe fournis par le labo.
8.  Ouvrez le **CMD**, exécutez la commande **ipconfig**, puis notez l’adresse IP.
9.  Revenez au portail Entra et actualisez la page Connecteurs.

Vous devriez voir la machine virtuelle intégrée et l’adresse IP associée. Cela signifie que vous avez réussi à installer le connecteur.

## Tâche 3 : créer un partage sur le serveur de fichiers

Dans cette tâche, vous allez créer un partage SMB sur le serveur de fichiers local, accessible via GSA.

1. Vous devriez toujours vous trouver dans LON-SC2.
2. Ouvrez l’**Explorateur**, accédez au lecteur C: et créez un dossier nommé **Partager**.
3. Sélectionnez le dossier de partage et ouvrez les **propriétés**.
4. Sélectionnez **Partage**.
5. Sélectionnez **Partager...**.
6. Dans la liste déroulante, sélectionnez **Tout le monde**, puis **Ajouter**.
7. Sélectionnez **Partager**.
8. Sélectionnez **Non, définir le réseau auquel je suis connecté comme réseau privé**.

## Tâche 4 : configurer Accès rapide et affecter l’utilisateur

Pour permettre à vos utilisateurs et utilisatrices d’accéder au serveur de fichiers via le client GSA, vous devez activer Accès rapide et l’affecter à vos utilisateurs et utilisatrices de test. Sans cette configuration, l’utilisateur ou l’utilisatrice de test ne pourra pas se connecter au serveur de fichiers.

1. Dans le volet de navigation de gauche, développez **Applications** et sélectionnez **Accès rapide**. Saisissez les informations suivantes :
    - Nom : **SMB vers ContosoFS**
    - Groupe de connecteurs : **Par défaut**
1. Sélectionnez **Ajouter un segment d’application Accès rapide** et renseignez les informations suivantes :
    - Type de destination : adresse IP
    - Adresse IP : « **ADRESSE IP DE VOTRE MACHINE VIRTUELLE** »
    - Ports : 445
1. Sélectionnez **Appliquer**.
1. Sélectionnez **Enregistrer** et recharger le menu Accès rapide.
1. Dans le volet de gauche, sélectionnez **Utilisateurs et groupes**.
1. Sélectionner **Ajouter un utilisateur/groupe**.
1. Sélectionnez **Aucun sélectionné**.
1. Ajoutez **Administrateur MOD**.
1. Cliquez sur **Sélectionner** > **Affecter**.

Vous avez activé Accès rapide pour votre utilisateur ou utilisatrice de test, dans ce cas votre compte Administrateur.

## Tâche 5 : Entra ID de jointure d’appareil

Pour utiliser Accès global sécurisé, vous devez joindre le point de terminaison client à Entra ID. Sinon, le client GSA ne fonctionnera pas.

1. Connectez-vous à LON-SC1, ouvrez le menu Démarrer et sélectionnez **Paramètres**.
2. Sélectionnez **Comptes** > **Accès professionnel ou scolaire**.
3. Pour ajouter un compte professionnel ou scolaire, sélectionnez **Se connecter**.
4. Cliquez sur **Joindre un appareil à Entra ID**.
5. Connectez-vous avec les informations d’identification d’**administrateur MOD** fournies par le fournisseur de labo.

Une fois que votre point de terminaison est joint à Entra ID, vous pouvez utiliser le client GSA pour vous connecter à toutes les ressources que vous protégez avec Accès global sécurisé.

## Tâche 6 : activer le profil et valider la connexion

Accès global sécurisé est divisé en deux parties. La partie sur laquelle vous travaillez s’appelle Accès privé et sécurise vos ressources locales et privées, telles que les serveurs de fichiers ou les applications locaux. Pour activer l’accès à votre serveur de fichiers, vous devez activer le profil d’accès privé qui permet aux utilisateurs et utilisatrices d’accéder aux ressources qui leur sont affectées via Accès rapide.

1. Dans le menu Accès global sécurisé, dans le volet de navigation de gauche du centre d’administration Microsoft Entra, développez **Se connecter** et choisissez **Transfert de trafic**.
2. Vérifiez le **profil d’accès privé**.
3. Cliquez sur **OK**.
4. Dans le volet de navigation de gauche, sous **Se connecter**, choisissez **Téléchargement du client**.
5. Sous Windows 10/11, sélectionnez **Télécharger le client**.
6. Installez le **client Accès global sécurisé**.
7. Pendant le processus d’installation, vous devez vous connecter avec votre administrateur MOD.
8. Ouvrez l’**Explorateur** dans Windows, accédez à la barre de menus **Ce PC**, sélectionnez les points de suspension (...), puis sélectionnez **Mapper le lecteur réseau**.
9. Dossier : `\\IP-ADDRESS\Share` utilisez l’adresse IP que vous avez notée précédemment.
10. Sélectionnez **Terminer**.
11. Entrez le nom d’utilisateur local et le mot de passe pour mapper le lecteur réseau.


Vous avez établi une connexion au serveur de fichiers à l’aide d’Accès global sécurisé.
