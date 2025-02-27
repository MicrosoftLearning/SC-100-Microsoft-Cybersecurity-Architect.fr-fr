# Sécurité des points de terminaison

Contoso utilise Microsoft Intune pour gérer ses appareils et fournit à ses employés des appareils Windows 10 et Windows 11. L’entreprise a implémenté plusieurs profils de configuration dans le passé. Toutefois, une analyse de l’infrastructure à l’échelle de l’entreprise a révélé que les stratégies actuelles ont été créées indépendamment. Il est donc difficile d’en avoir une vue d’ensemble et d’en effectuer le suivi. En tant qu’architecte cyber-sécurité de l’entreprise, vous avez décidé de consolider toutes les configurations nécessaires et critiques en un seul endroit. 

En outre, l’analyse a révélé que Tailwind Traders utilise des appareils macOS dans son environnement. Dans le cadre de la fusion à venir, vous prévoyez de préparer le locataire Contoso pour les nouveaux appareils macOS.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour relever les défis auxquels Contoso Ltd est confronté.

### Approche de conception

Dans ce scénario, les exigences suivantes peuvent s’avérer pertinentes :

- Consolider toutes les configurations pour les appareils Windows en un seul endroit
- Protéger les appareils macOS

Microsoft Endpoint Manager, avec des bases de référence de sécurité, gère et sécurise de manière centralisée les points de terminaison, notamment les ordinateurs de bureau, les ordinateurs portables, les appareils mobiles et les serveurs. Il intègre des outils tels qu’Intune et Configuration Manager, permettant un déploiement efficace des applications, l’application des stratégies, la conformité et la surveillance des appareils. 

Une stratégie de base de référence de sécurité comprend un ensemble de paramètres de configuration recommandés par Microsoft, détaillant leurs implications en matière de sécurité. Ces paramètres sont basés sur les commentaires des équipes d’ingénieurs de Sécurité Microsoft, des groupes de produits, des partenaires et des clients et clientes. Ces bases de référence englobent des paramètres de configuration d’appareil similaires à ceux de différentes stratégies Intune. La personnalisation de chaque base de référence déployée permet l’application des paramètres et des valeurs nécessaires. Pour établir un profil de base de référence de sécurité dans Intune, vous créez un modèle comprenant plusieurs profils de configuration d’appareil. Ces recommandations doivent être régulièrement examinées et adaptées en fonction des différentes exigences métier.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Consolider toutes les configurations pour les appareils Windows en un seul endroit|Microsoft Endpoint Manager - Sécurité des points de terminaison|Déployer des stratégies de base de référence de sécurité
|Protéger les appareils macOS|Microsoft Endpoint Manager|Déployer un antivirus sur les appareils macOS|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : déployer des stratégies de base de référence de sécurité de point de terminaison

Votre objectif global est de sécuriser vos points de terminaison de manière appropriée et de consolider autant de stratégies que possible en un seul endroit. Pour ce faire, vous allez créer des stratégies de base de référence de sécurité de point de terminaison pour les appareils Windows dans Intune.

1. Connectez-vous à la machine virtuelle cliente Windows **LON-SC1** avec le compte **Administrateur** local. Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Connectez-vous au Centre d’administration Microsoft Intune **`https://intune.microsoft.com`** en tant qu’**administrateur MOD**admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
1. Si vous voyez une zone d’informations en haut à droite de l’écran qui indique **Gérer l’authentification multifacteur**, fermez-la en cliquant sur le **X**.
1. Dans le centre d’administration Microsoft Intune, sélectionnez **Sécurité des points de terminaison** dans le volet de navigation de gauche.
1. Sur la page **Sécurité des points de terminaison | Vue d’ensemble**, sous **Vue d’ensemble**, sélectionnez **Bases de référence de sécurité**.
1. Sur la page **Sécurité des points de terminaison | Bases de référence de sécurité**, sélectionnez **Base de référence de sécurité pour Windows 10 et versions ultérieures**.
1. Sur la page **Base de référence de sécurité pour Windows 10 et versions ultérieures | Profils**, sélectionnez **+ Créer un profil**.
1. Passez en revue la description dans le panneau **Créer un profil**, puis sélectionnez **Créer**.
1. Dans le panneau **De base**, entrez :
    1. Nom : **`Secure Windows Endpoints`**
    1. Description : **`The Security Baseline for Windows 10 and later represents the recommendations for configuring Windows.`**.
1. Cliquez sur **Suivant**.
1. Dans le panneau **Paramètres de configuration**, examinez les différentes options de configuration. Lorsque vous avez terminé, sélectionnez **Suivant**.
1. Dans le panneau **Balises de portée**, sélectionnez **Suivant**.
1. Dans le panneau **Affectations**, sous **Groupes inclus**, sélectionnez **Ajouter tous les utilisateurs**, puis **Suivant**.
1. Dans le panneau **Examiner et créer**, sélectionnez **Créer**.
1. Revenez à la page **Sécurité des points de terminaison | Bases de référence de sécurité**.
1. Sur la page **Sécurité des points de terminaison | Bases de référence de sécurité**, sélectionnez **Base de référence de sécurité Microsoft Defender pour point de terminaison**.
1. Sur la page **Base de référence de sécurité Microsoft Defender pour point de terminaison | Profils**, sélectionnez **+ Créer un profil**.
1. Passez en revue la description dans le panneau **Créer un profil**, puis sélectionnez **Créer**.
1. Dans le panneau **De base**, entrez :
    1. Nom : **`Defender for Endpoint Security Baseline`**
    1. Description : **`Security best practices for the Microsoft security stack on devices managed by Intune`**.
1. Cliquez sur **Suivant**.
1. Dans le panneau **Paramètres de configuration**, examinez les différentes options de configuration. Lorsque vous avez terminé, sélectionnez **Suivant**.
1. Dans le panneau **Balises de portée**, sélectionnez **Suivant**.
1. Dans le panneau **Affectations**, sous **Groupes inclus**, sélectionnez **Ajouter tous les utilisateurs**, puis **Suivant**.
1. Dans le panneau **Examiner et créer**, sélectionnez **Créer**.

Vous avez créé deux stratégies de base de référence de sécurité pour les appareils Windows.

### Tâche 2 : déployer un antivirus sur les appareils macOS

Après avoir sécurisé les appareils Windows avec des stratégies de base de référence de sécurité de point de terminaison, vous allez déployer un antivirus et activer le chiffrement sur les appareils macOS pour préparer votre environnement à la fusion avec Trailwind Traders.

1. Vous devrier toujours vous trouver dans le centre d’administration Microsoft Intune **https://intune.microsoft.com**.
1. Dans le centre d’administration Microsoft Intune, sélectionnez **Sécurité des points de terminaison** dans le volet de navigation de gauche.
1. Sur la page **Sécurité des points de terminaison | Vue d’ensemble**, sous **Gérer**, sélectionnez **Antivirus**.
1. Sur la page **Sécurité des points de terminaison | Antivirus**, sélectionnez **+ Créer une stratégie**.
1. Dans le volet **Créer un profil**, sous **Plateforme**, sélectionnez **macOS** et sous **Profil**, sélectionnez **Microsoft Defender Antivirus**.
1. Sélectionnez **Créer**.
1. Dans le panneau **De base**, entrez :
    1. Nom : **`Deploy antivirus on macOS devices`**
    1. Description : **`Deploy antivirus and enable encryption on macOS devices to prepare your environment for merging with Trailwind Traders.`**
1. Sélectionnez **Suivant**.
1. Dans l’onglet **Paramètres de configuration**, vérifiez que les paramètres sont configurés comme suit :
1. Sous **Préférences de protection fournies par le cloud** :
    - Activer/désactiver la protection fournie par le cloud : **activé (par défaut)**
    - Activer/désactiver les exemples d’envois automatiques : **activé (par défaut)**
    - Niveau de collecte de diagnostic : **facultatif (par défaut)**
    - Mise à jour automatique de la veille de sécurité : **activé (par défaut)**
1. Sous **Moteur antivirus** :
    - Activer la protection en temps réel : **activé (par défaut)**
    - Activer le mode passif : **désactivé (par défaut)**
    - Fusion d’exclusion : **admin_only**
1. Sous **Paramètres de type de menace**, sélectionnez **+ Ajouter** :
    - Dans la zone de texte du type de menace, entrez : **potentially_unwanted_application**
    - Action à entreprendre : **bloquer**
    - Fusion des paramètres de type de menace : **admin_only**
1. Activer le calcul de hachage de fichier : **True****
1. Exécuter une analyse après la mise à jour des définitions : **activé (par défaut)**
1. Niveau d’application : **real_time**
1. Sous **Protection réseau** :
    - Niveau d’application : bloquer
1. Sous **Protection contre les falsifications** :
    - Niveau d’application : **bloquer (par défaut)**
1. Sous **Préférences d’interface utilisateur**
    - Contrôler la connexion à la version du consommateur : **activé (par défaut)**
    - Afficher/masquer l’icône de menu d’état : **désactivé (par défaut)**
    - Commentaires initiés par l’utilisateur : **activé (par défaut)**
1. Cliquez sur **Suivant**.
1. Dans le panneau **Balises de portée**, sélectionnez **Suivant**.
1. Dans l’onglet **Affectations**, dans la zone de texte, entrez **Tous les utilisateurs** et sélectionnez-le.
1. Cliquez sur **Suivant**.
1. Dans l’onglet **Examiner et créer**, sélectionnez **Enregistrer**.

Vous avez correctement configuré et déployé l’antivirus sur les appareils macOS.

### Tâche 3 : chiffrer les appareils macOS

Dans cette tâche, vous allez chiffrer les appareils macOS.

1. Vous devrier toujours vous trouver dans le centre d’administration Microsoft Intune **https://intune.microsoft.com**.
1. Dans le centre d’administration Microsoft Intune, sélectionnez **Sécurité des points de terminaison** dans le volet de navigation de gauche.
1. Sur la page **Sécurité des points de terminaison | Vue d’ensemble**, sous **Gérer**, sélectionnez **Chiffrement de disque**.
1. Sur la page **Sécurité des points de terminaison | Chiffrement de disque**, sélectionnez **+ Créer une stratégie**.
1. Dans le volet **Créer un profil**, sous **Plateforme**, sélectionnez **macOS** et sous **Profil**, sélectionnez **FileVault**.
1. Sélectionnez **Créer**.
1. Dans le panneau **De base**, entrez :
    1. Nom : **`Encrypt macOS devices`**
    1. Description : **`FileVault provides built-in Full Disk Encryption for macOS devices.`**
    1. Cliquez sur **Suivant**.
1. Dans le panneau **Paramètres de configuration**, sous **Chiffrement**, configurez les paramètres suivants :
   - Activer FileVault : **oui**
   - Rotation des clés de récupération personnelles : **6 mois**
   - Description de l’emplacement de dépôt de la clé de récupération personnelle : **`To recover a lost or recently rotated recovery key, log in to the Intune Company Portal website using any device. Navigate to the Devices section within the portal, choose the device with FileVault enabled, and then select the option to retrieve the recovery key. The portal will display the current recovery key for that device.`**
   - Nombre de fois autorisé à contourner : **3**
   - Autoriser le report jusqu’à la déconnexion : **oui**
   - Désactiver l’invite lors de la déconnexion : **oui**
   - Masquer la clé de récupération : **oui**
   - Cliquez sur **Suivant**.
1. Dans le panneau **Balises de portée**, sélectionnez **Suivant**.
1. Dans le panneau **Affectations**, sous **Groupes inclus**, sélectionnez **Ajouter tous les utilisateurs**, puis **Suivant**.
1. Dans le panneau **Examiner et créer**, sélectionnez **Créer**.

Vous avez correctement configuré et déployé un profil FileVault pour chiffrer les appareils macOS.
