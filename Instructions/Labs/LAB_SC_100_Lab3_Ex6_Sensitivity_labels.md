---
lab: 3
title: "Exercice\_6 - Étiquettes de confidentialité"
---

# Labo 3 - Exercice 6 - Étiquettes de confidentialité

Contoso Ltd. est en train d’acquérir Tailwind Traders. La direction a décidé de traiter tous les documents du processus comme strictement confidentiels afin de réduire le risque de fuite de données.

Vous avez reçu les exigences de sécurité suivantes pour l’étiquette :

- Le contenu peut uniquement être partagé avec les employés internes de Contoso Ltd.
- Le contenu doit être chiffré.
- Les fichiers et les e-mails peuvent ne pas être transférés.
- L’accès au contenu à partir d’appareils non professionnels est interdit.
- La portée de cette étiquette est la direction.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour résoudre les problèmes auxquels Contoso Ltd est confronté.

### Approche de conception

Contoso a plusieurs solutions en place pour protéger ses données. Votre première approche consiste à analyser la configuration existante et à décider si elle répond aux exigences actuelles. 

En fonction du scénario ci-dessus, vous pouvez utiliser Protection des données Microsoft Purview pour répondre aux exigences et protéger correctement les données. Les étiquettes de confidentialité de Protection des données Microsoft Purview vous permettent de classifier et de protéger les données de votre organisation, tout en garantissant la productivité des utilisateurs et utilisatrices et le maintien des capacités de collaboration. 

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Chiffrer des documents et des e-mails|Protection des informations Microsoft Purview|Déployer une étiquette de confidentialité|
|Restreindre l’accès aux données à partir d’appareils non gérés|Protection des informations Microsoft Purview|Déployer une étiquette de confidentialité|
|Restreindre l’accès aux utilisateurs et utilisatrices internes|Protection des informations Microsoft Purview|Déployer une étiquette de confidentialité

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : examiner les étiquettes de confidentialité actuelles

Dans cette tâche, vous allez examiner les étiquettes de confidentialité actuelles et déterminer s’il est nécessaire d’en créer une nouvelle.

>[!NOTE] Vous devez avoir déjà installé le module PowerShell Exchange Online. Si ce n’est pas le cas, suivez les instructions d’installation du module.

1. Ouvrez une fenêtre PowerShell à privilèges élevés, en cliquant avec le bouton droit de la souris sur le bouton Windows et en sélectionnant **Windows PowerShell (administration)**.
1. Dans la fenêtre **Contrôle de compte d’utilisateur**, confirmez en cliquant sur **Oui**.
1. Saisissez la cmdlet suivante pour installer la dernière version du module PowerShell Exchange Online :

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirmez la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur **O** pour Oui, puis appuyez sur **Entrée**.  Ce processus peut prendre un certain temps.
1. Entrez la cmdlet suivante pour vous connecter à Security &Compliance PowerShell :

    ```powershell
    Connect-IPPSSession
    ```
1. Lorsque la fenêtre **Connexion** s’affiche, connectez-vous en tant que admin@WWLxZZZZZZ.onmicrosoft.com (où ZZZZZZZ est votre ID de locataire unique fourni par votre hébergeur de labo) et utilisez le mot de passe d’administration de votre locataire.
1. Entrez la cmdlet suivante pour obtenir la liste de tous les déploiements d’étiquettes de confidentialité :

    ```powershell
    Get-Label | Format-Table -wrap ParentLabelDisplay,DisplayName,LabelActions
    ```
Cette cmdlet affiche toutes les étiquettes de confidentialité déployées et les actions correspondantes. Examinez les étiquettes. Déterminez si les étiquettes existantes répondent aux exigences de l’entreprise ou s’il est nécessaire d’en créer une nouvelle. Une fois que vous avez terminé, passez à la tâche suivante.

### Tâche 2 : activer la prise en charge des étiquettes de confidentialité pour les groupes et les sites

Dans une tâche précédente, vous avez examiné les étiquettes existantes et vous avez conclu qu’elles ne répondent pas aux exigences de l’entreprise. Pour appliquer des étiquettes de confidentialité aux groupes et sites, vous devez activer la prise en charge des étiquettes de confidentialité dans PowerShell.

1. Ouvrez une fenêtre PowerShell à privilèges élevés en cliquant sur le menu Démarrer avec le bouton droit de la souris, puis sélectionnez Windows PowerShell et exécutez en tant qu’administrateur.
1. Dans la fenêtre Contrôle de compte d’utilisateur, confirmez en cliquant sur Oui, puis appuyez sur Entrée.
1. Tout d’abord, nous devons installer le kit de développement logiciel (SDK) Microsoft Graph PowerShell. Nous devons installer les deux modules qu’il inclut : Microsoft.Graph et Microsoft.Graph.Beta. Entrez la cmdlet suivante pour installer la dernière version de Microsoft.Graph :

```powershell
Install-Module Microsoft.Graph -Scope CurrentUser
```
1. Confirmez la boîte de dialogue de sécurité Nuget et la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur Y pour Oui, puis appuyez sur Entrée. Ce processus peut prendre un certain temps.
1. Entrez la cmdlet suivante pour installer Microsoft.Graph.Beta :

```powershell
Install-Module Microsoft.Graph.Beta -Scope CurrentUser
```
1. Dans la fenêtre Contrôle de compte d’utilisateur, confirmez en cliquant sur Oui, puis appuyez sur Entrée.
1. Connectez-vous au locataire :

```powershell
Connect-MgGraph -Scopes "Directory.ReadWrite.All"
```

1. Dans le formulaire de connexion à votre compte, connectez-vous en tant que admin@WWLxZZZZZZ.onmicrosoft.com, (où ZZZZZZ est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
1. Dans la fenêtre **Autorisations demandées**, sélectionnez **Consentir au nom de votre organisation**, puis **Accepter**. Après la connexion, choisissez la fenêtre PowerShell.
1. Entrez la cmdlet suivante pour activer les étiquettes de confidentialité :

```powershell
$params = @{
     Values = @(
        @{
            Name = "EnableMIPLabels"
            Value = "True"
        }
     )
}

Update-MgBetaDirectorySetting -DirectorySettingId $grpUnifiedSetting.Id -BodyParameter $params
```

1. Fermez la fenêtre PowerShell.

Vous avez activé la prise en charge des étiquettes de confidentialité pour les groupes et les sites.

### Tâche 3 : créer et déployer une étiquette de confidentialité haute sécurité

Vous allez créer une étiquette de confidentialité pour répondre aux exigences.

1. Connectez-vous au portail de conformité Microsoft Purview **https://compliance.microsoft.com/** en tant qu’Allan Deyoung à l’aide de son compte **Administrateur MOD**.
1. Dans le portail Microsoft Purview, dans le volet de navigation de gauche, développez **Information Protection**, puis sélectionnez **Étiquettes**.
1. Sur la page **Étiquettes**, sélectionnez **+ Créer une étiquette**.
1. Sur la page **Fournir des détails de base pour cette étiquette**, entrez les informations suivantes :

    - **Nom** : confidentiel - processus d’acquisition
    - **Nom d’affichage** : confidentiel - processus d’acquisiton
    - **Description pour les utilisateurs** : données hautement confidentielles liées à tout processus d’acquisiton.
    - **Description pour l’équipe d’administration** : cette étiquette protège toutes les données liées aux acquisitons de Contoso.

1. Cliquez sur **Suivant**.
1. Dans la page **Définir la portée de cette étiquette**, sélectionnez **Éléments**, puis **Fichiers**, **E-mails**, et **Groupes et sites**. Si d’autres options de cette page sont sélectionnées, désélectionnez-les.
1. Sur la page **Choisir les paramètres de protection pour les éléments étiquetés**, sélectionnez **Appliquer ou supprimer le chiffrement**.
1. Sur la page **Chiffrement**, sélectionnez **Configurer les paramètres de chiffrement**.
1. Dans les paramètres de chiffrement, entrez les informations suivantes : 
    - **Attribuer des autorisations maintenant ou autoriser les utilisateurs et utilisatrices décider ?**  : permettre aux utilisateurs et utilisatrices d’attribuer des autorisations lorsqu’ils appliquent l’étiquette.
    - **Dans Outlook, appliquez l’une des restrictions suivantes** : Ne pas transférer.
1. Sélectionnez **Dans Word, PowerPoint et Excel, invitez les utilisateurs et utilisatrices à spécifier des autorisations**, puis sélectionnez **Suivant**.
1. Sur la page **Étiquetage automatique des fichiers et des e-mails**, sélectionnez **Suivant**.
1. Sur la page **Définir les paramètres de protection pour les groupes et les sites**, sélectionnez **Confidentialité et accès utilisateur externe**, **Partage externe et accès conditionnel**, puis **Suivant**.
1. Sur la page **Paramètres de confidentialité des données et d’accès utilisateur externe**, sélectionnez **Privé**, puis **Suivant**.
1. Sur la page **Définir les paramètres de partage externe et d’accès conditionnel**, sélectionnez **Contrôler le partage externe à partir de sites SharePoint étiquetés** et **Utiliser l’accès conditionnel Microsoft Entra pour protéger les sites SharePoint étiquetés** et configurez comme suit :
    - **Le contenu existant peut être partagé avec** : uniquement des personnes de votre organisation.
    - **Déterminer si les utilisateurs et les utilisatrices peuvent accéder aux sites SharePoint à partir d’appareils non gérés** : Bloquer l’accès
1. Cliquez sur **Suivant**.
1. Sur la page **Étiquetage automatique des ressources de données schématisées (version préliminaire)**, sélectionnez **Suivant**.
1. Sur la page **Vérifier les paramètres et terminer**, sélectionnez **Créer une étiquette**.
1. Sur la page **Votre étiquette de confidentialité a été créée**, sélectionnez **Publier une étiquette sur les applications des utilisateurs**.
1. Cliquez sur **Terminé**.
1. Sur la page **Publier une étiquette**, sélectionnez **Créer une stratégie d’étiquette**.
1. Sur la page **Choisir l’étiquette de confidentialité à publier**, sélectionnez l’étiquette que vous venez de créer, puis **Suivant**.
1. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**.
1. Sur la page **Publier sur les utilisateurs et les groupes**, sélectionnez **Utilisateurs et groupes**, puis **Modifier**.
1. Sur la page **Portée des utilisateurs et des groupes**, sélectionnez **Utilisateurs et groupes spécifiques**, puis **+ Inclure des utilisateurs et des groupes**, puis **Cadres** et **Direction**, puis sélectionnez **Terminé** jusqu’à ce que l’affectation d’utilisateurs soit terminée.
1. Cliquez sur **Suivant**.
1. Sur la page **Paramètres de stratégie**, sélectionnez **Les utilisateurs doivent fournir une justification pour supprimer une étiquette** et **Les utilisateurs doivent appliquer une étiquette à leurs e-mails et documents**.
1. Cliquez sur **Suivant**.
1. Sur la page **Paramètres par défaut des documents**, sélectionnez **L’e-mail hérite de l’étiquette de priorité la plus élevée des pièces jointes**, puis **Suivant**.
1. Sur la page **Paramètres par défaut des réunions et des événements de calendrier**, sélectionnez **Suivant**.
1. Sur la page **Paramètres par défaut des groupes et des sites**, sélectionnez **Suivant**.
1. Sur la page **Paramètres par défaut du contenu Fabric et Power BI**, sélectionnez **Suivant**.
1. Sur la page **Nommer votre stratégie**, entrez les informations suivantes :
    - **Nom** : Sstratégie d’étiquette de confidentialité de direction
    - **Description** : cette stratégie de protection est conçue pour la direction dans le cadre de l’acquisition d’entreprises
1. Cliquez sur **Suivant**.
1. Dans la page **Vérifier et terminer**, sélectionnez **Envoyer**.

Vous avez créé et publié une étiquette de confidentialité.