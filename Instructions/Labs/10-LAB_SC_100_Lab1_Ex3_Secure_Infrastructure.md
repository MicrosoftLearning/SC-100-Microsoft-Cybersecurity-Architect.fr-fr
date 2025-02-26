# Infrastructure sécurisée

Contoso Ltd. a récemment acquis Tailwind Traders, une société qui utilise encore des serveurs de fichiers locaux pour son stockage. En tant qu’architecte en cybersécurité de Contoso Ltd., vous souhaitez évaluer une solution pour sécuriser ces serveurs de fichiers avec votre environnement cloud existant. Tailwind Traders vous a fourni un serveur de test (le Lab VM 2) que vous pouvez utiliser pour implémenter votre POC. Dans cet exercice, vous allez configurer le serveur et l’intégrer dans votre environnement de sécurité et infrastructure cloud à l’aide d’Azure Arc et envoyer les journaux du serveur à Defender pour le Cloud.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour sécuriser l’environnement local à l’intérieur de votre infrastructure cloud.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Activer Defender for Cloud dans votre abonnement
- Les serveurs locaux doivent être sécurisés
- Les journaux doivent être stockés de manière à pouvoir être traités par la solution SIEM de Contoso
- Évaluer l’état de conformité des ressources de déploiement

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Defender for Cloud fournit des recommandations pour sécuriser les ressources cloud et locales en identifiant les étapes permettant d’améliorer la configuration et le déploiement. La surveillance active des charges de travail améliore la posture globale de sécurité et réduit l’exposition aux menaces.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Activer Defender for Cloud dans votre abonnement| Defender pour le cloud | Activer les plans Defender dans Defender pour le cloud |
|Les serveurs locaux doivent être sécurisés | Azure Arc | Intégrer le serveur local à l’environnement cloud |
|Les journaux doivent être stockés de manière à ce que la solution SIEM de Contoso puisse les traiter |Defender pour le cloud, DataCollectionRules, AzureMonitoring Agent, espace de travail Log Analytics | Créer une règle de collecte de données pour collecter des journaux à partir du serveur local de Contoso |
|Évaluer l’état de conformité des ressources de déploiement | Politiques de sécurité de Defender pour le cloud| Activez la conformité NIST SP 800-53 Rev.5 et évaluez votre état de conformité.|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : créer un espace de travail Log Analytics

Dans cette tâche, vous allez créer un espace de travail Log Analytics pour héberger les données envoyées par différentes ressources.

1. Connectez-vous à la machine virtuelle Client 1 (LON-SC1) en tant que compte **lon-sc1\admin** . Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresses, accédez à **`https://portal.azure.com`** et connectez-vous au Portail Azure en tant que **User1-*******@LODSUATMCA.onmicrosoft.com** (où ****** est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
1. Dans la boîte de dialogue Rester connecté ?, cochez la case Ne plus afficher, puis sélectionnez **Non**.
1. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant Jamais, pour ne pas enregistrer les informations d’identification des administrateurs généraux par défaut dans votre navigateur.
1. Dans l’écran Bienvenue dans Microsoft Azure, sélectionnez Annuler.
1. Sélectionnez **Créer une ressource** et cherchez **Espace de travail Log Analytics**
1. Cherchez la **vignette Espace de travail Log Analytics**, sélectionnez **Créer**.
1. Sur la page Créer un espace de travail Log Analytics, créez un **Groupe de ressources** et nommez-le **`ContosoRG`**.
1. Dans les détails de l’instance, entrez le nom **`ContosoLA`** et sélectionnez la région **USA Est**.
1. Sélectionnez **Vérifier et créer**
1. Sélectionnez **Créer** pour démarrer le déploiement.

L’espace de travail Log Analytics a bien été créé.

### Tâche 2 : activer Defender pour le cloud

Avant que Defender pour le cloud puisse appliquer des protections à vos ressources, vous devez activer les plans Defender pour les types de ressources que vous souhaitez sécuriser.

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Recherchez **Microsoft Defender pour le cloud** et ouvrez-le.
1. Dans le volet de navigation de gauche, développez **Gestion** et sélectionnez **Paramètres d’environnement**.
1. Sélectionnez **Tout développer** puis sélectionnez votre abonnement.
1. Si l’abonnement figure comme **non enregistré**, rechargez la page.
1. Sélectionnez les points de suspension (...) en regard de l’abonnement, puis sélectionnez **Modifier les paramètres**.
1. Sous **Protection de charge de travail cloud**, définissez le plan **Serveurs** sur la droite sur **Activé**.
1. En haut de la page, sélectionnez **Enregistrer**.

Lorsque vous activez le plan pour serveurs, vous pouvez voir que Defender pour le cloud prend en charge un grand nombre de types de ressources supplémentaires.

### Tâche 3 : Activer le serveur local dans Azure Arc

Azure Arc est requis pour envoyer des données à l’espace de travail Log Analytics utilisé par Defender pour le cloud.

1. Accédez à la machine virtuelle **LON-SC2** et connectez-vous au Portail Azure **`https://portal.azure.com`**.
1. Cherchez **`Azure Arc`** et ouvrez-le.
1. Dans le volet de navigation de gauche, développez **Ressources Azure Arc** et sélectionnez **Machines**.
1. Sélectionnez **Ajouter/Créer** > **Ajouter une machine.**
1. Dans la section Ajouter un serveur unique, sélectionnez **Générer un script**.
1. Dans le champ Groupe de ressources, utilisez le menu déroulant pour sélectionner **ContosoRG**.
1. Dans le champ Région, utilisez le menu déroulant pour sélectionner **USA Est**.
1. Sélectionnez **Télécharger et exécuter le script**.
1. Sélectionnez **Télécharger** et exécutez le script sur votre deuxième client de labo **LON-SC2** pour intégrer le serveur local à Azure.
1. Exécutez Windows PowerShell en tant qu’administrateur. Pour cela, utilisez le bouton droit de la souris pour sélectionner l’icône Windows en bas à droite de la fenêtre, puis sélectionnez **Windows PowerShell (Admin)**
1. Définissez la stratégie d’exécution sur « non restreint ».

    ```Powershell
    Set-ExecutionPolicy -ExecutionPolicy unrestricted
    ```

1. Dans les fenêtres PowerShell, sélectionnez Y
1. Exécutez le script d’intégration. Pour cela, sélectionnez Explorateur de fichiers. Vous accédez alors au dossier des téléchargements du lecteur C local de la machine virtuelle du serveur. Utilisez le bouton droit de la souris pour sélectionner le fichier **OnboardingScript** et sélectionnez **Exécuter avec **PowerShell**.
1. Lorsque la fenêtre contextuelle d’authentification s’affiche, connectez-vous avec le même compte que celui que vous utilisez pour le Portail Azure.
1. Attendez que l’exécution du script se termine.
1. Revenez à LON-SC1 et ouvrez Azure Arc.
1. Sélectionnez **Machines** puis **Actualiser** en haut de la page et vérifiez que votre serveur est correctement déployé sur Azure Arc.

Vous avez activé Azure Arc sur le serveur de test et les données doivent maintenant commencer à circuler dans l’espace de travail Log Analytics. Il peut s’écouler un certain temps avant que les données apparaissent dans le tableau de bord.

### Tâche 4 : ajouter un serveur à Defender pour le cloud et collecter des journaux.

Vous allez déployer une règle de collecte de données pour obtenir les journaux des événements du serveur local. La règle déploie automatiquement l’agent de surveillance sur le serveur et transfère les journaux à l’espace de travail Log Analytics créé précédemment.

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Ouvrez Defender pour le cloud.
1. Dans le volet de navigation de gauche, développez **Gestion** et sélectionnez **Paramètres d’environnement**.
1. Sélectionnez **Développer tout**.
1. Vous verrez l’espace de travail Log Analytics créé précédemment, **ContosoLA**.  
1. Sélectionnez les points de suspension (...) de l’élément **ContosoLA**, puis sélectionnez **Modifier les paramètres**.
1. Définissez le plan **Serveurs** sur la droite sur **Activé**.
1. En haut de la page, sélectionnez **Enregistrer**.
1. Utilisez la barre de recherche en haut pour rechercher la **règle Données de collecte**, puis sélectionnez-la dans les résultats de la recherche.
1. Sélectionnez **Créer**.
1. - Nom de la règle : **`ContosoDCR`**
   - Groupe de ressources : **ContosoRG**
1. Sélectionnez **Suivant : Ressources**.
1. Sélectionnez **Ajouter des ressources**. Développez l’étendue du groupe de ressources. Cochez la machine Azure Arc précédemment intégrée puis sélectionnez **Appliquer**.
1. Sélectionnez **Suivant : Collecter et livrer**.
1. Sélectionnez **Ajouter une source de données**.
1. Sélectionnez le type de source de données **Journaux des événements Windows**.
1. Sélectionnez chaque option sous **Configurer les journaux d’événements et les niveaux à collecter :**.
1. Sélectionnez **Suivant : Destination**.
1. Sélectionnez **Ajouter une destination**.
   - Type de destination : **Journaux Azure Monitor**
   - Compte ou espace de noms : **ContosoLA**
1. Sélectionnez **Ajouter une source de données**.
1. Sélectionnez **Vérifier et créer**.
1. Sélectionnez **Créer**.

Il se peut s’écouler quelques heures avant que la ressource ne soit entièrement intégrée dans Defender pour le cloud. L’étape suivante consiste à examiner la recommandation que Defender pour le cloud génère pour cette ressource.

### Tâche 5 : ajouter une norme de conformité réglementaire

En fonction de la recommandation, vous pouvez commencer à sécuriser la ressource et à affecter des stratégies de sécurité, par exemple NIST SP 800-53 Rev.5 pour vous assurer que les ressources de Tailwind Traders respectent nos réglementations de conformité.

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Ouvrez Defender pour le cloud, développez **Gestion** et sélectionnez **Paramètres d’environnement**.
1. Sélectionnez **Développer tout**.
1. Sélectionnez les points de suspension (...) en regard de l’abonnement, puis sélectionnez **Modifier les paramètres**.
1. Dans le menu de navigation de gauche, sélectionnez **Stratégies de sécurité**. Le chargement de la liste peut prendre un certain temps.
1. Recherchez **`NIST SP 800-53 Rev. 5`**. Déplacez le curseur d’état sur **Activé**.
1. Revenez à Defender pour le cloud, développez **Sécurité du cloud**, puis sélectionnez **Conformité réglementaire**.

En raison des limitations de l’environnement de labo, vous ne pouvez pas voir les ressources ni les recommandations de conformité. Cela prend un certain temps jusqu’à ce que les ressources déployées soient visibles dans Defender pour le cloud.

Dans le tableau de bord Conformité réglementaire, vous pouvez maintenant passer en revue les évaluations ayant échoué dans le tableau de bord pour connaître les recommandations.

En évaluant en permanence les ressources avec ces contrôles, Defender pour le cloud identifie les problèmes susceptibles d’entraver l’obtention de certificats de conformité spécifiques. Le maintien de la conformité réglementaire est essentiel pour protéger les données de votre organisation et garantir un environnement cloud sécurisé.
