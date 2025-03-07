# Stratégies de rétention

Le gouvernement allemand a récemment modifié des lois régissant les périodes de rétention pour les entreprises. L’un des principaux changements est que tous les documents financiers doivent maintenant être conservés pendant 11 ans, au lieu de 10 ans auparavant. Un autre changement essentiel est que les correspondances de l’entreprise, y compris les copies des correspondances de l’entreprise distribuée, peut maintenant être conservée pendant 5 ans au lieu de 7 ans. Actuellement, votre entreprise respecte une stratégie de rétention qui conserve tous les documents pendant une durée de 7 ans. Toutefois, Contoso Ltd. a rencontré des difficultés ces dernières années en raison de l’accumulation d’un grand volume de données dans son environnement. Cela a entraîné une augmentation des coûts de maintenance et une consommation importante d’espace de stockage. Votre objectif consiste à optimiser la stratégie de rétention de votre entreprise pour respecter les réglementations légales tout en réduisant les exigences de stockage des données. La stratégie de l’entreprise détermine que toutes les données doivent être conservées pendant au moins cinq ans après leur création, en respect strict de toutes les lois applicables régissant la conservation des données.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour relever les défis auxquels Contoso Ltd est confronté.

### Approche de conception

La première étape consiste à analyser les exigences en fonction du problème et à comprendre les objectifs.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Conserver toutes les données financières pendant 11 ans
- Conserver toutes les correspondances de l’entreprise pendant 5 ans
- Réduire la surcharge de stockage des données

La deuxième étape consiste à étudier l’environnement actuel de Contoso Ltd.. Contoso a plusieurs solutions en place pour conserver ses données pendant un certain temps. Votre tâche consiste à analyser la configuration actuelle et à décider si elle répond aux exigences légales. 

La troisième phase implique l’élaboration du concept de solution. Après examen approfondi, il devient évident qu’aucune des stratégies existantes ne répond aux critères spécifiés. Par conséquent, un nouvel ensemble de stratégies doit être créé.

Selon le scénario ci-dessus, vous pouvez utiliser Gestion du cycle de vie des données Microsoft Purview pour conserver les données de manière adéquate.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Conserver toutes les données financières pendant 11 ans| Gestion de cycle de vie des données Microsoft Purview|Créer une étiquette de rétention à application automatique|
|Conserver toutes les correspondances de l’entreprise pendant 5 ans| Gestion de cycle de vie des données Microsoft Purview|Déployer une stratégie de rétention|


## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : analyser la structure actuelle de la stratégie de rétention

Dans cette tâche, vous vous familiariserez avec la stratégie de rétention existante de votre entreprise. Vous allez examiner différentes stratégies de rétention, étiquettes et stratégies d’étiquette. Vous allez utiliser le module PowerShell Sécurité et conformité et afficher les stratégies existantes. Vous allez examiner la configuration actuelle et déterminer si les stratégies de rétention existantes sont suffisantes pour que Contoso Ltd. respecte les exigences légales.

>[!NOTE] Vous devez avoir déjà installé le module PowerShell Exchange Online. Si ce n’est pas le cas, suivez les instructions d’installation du module.

1. Ouvrez une fenêtre Windows PowerShell élevée en sélectionnant le bouton Windows avec le bouton droit de la souris, puis sélectionnez **Terminal (Admin)**.
1. Dans la fenêtre **Contrôle de compte d’utilisateur**, confirmez en cliquant sur **Oui**.
1. Saisissez la cmdlet suivante pour installer la dernière version du module PowerShell Exchange Online :

    ```powershell
    Install-Module ExchangeOnlineManagement
    ```
1. Confirmez la boîte de dialogue de sécurité du référentiel non approuvé en appuyant sur **O** pour Oui, puis appuyez sur **Entrée**.  Ce processus peut prendre un certain temps.
1. Entrez la cmdlet suivante pour vous connecter à Security &Compliance PowerShell, puis, lorsque vous y êtes invité, connectez-vous avec vos informations d’identification d’administrateur MOD :

    ```powershell
    Connect-IPPSSession
    ```

1. Entrez la cmdlet suivante pour afficher les stratégies et paramètres de rétention actuels :

    ```powershell
     Get-ComplianceTag | Format-Table -Auto Name,Priority,RetentionAction,RetentionDuration,Workload
    ```

1. Prenez le temps d’évaluer la table qui s’affiche.

    >[!NOTE] Vous pouvez également accéder au portail de conformité Microsoft Purview pour afficher les stratégies de rétention, mais vous devez examiner chaque stratégie une par une au lieu d’en obtenir une vue d’ensemble.

Vous avez correctement examiné les étiquettes et les paramètres existants pour déterminer s’ils répondent aux exigences légales.

### Tâche 2 : créer une stratégie de rétention

Vous avez évalué efficacement les stratégies de rétention de Contoso Ltd., et découvert une configuration obsolète qui ne répond pas aux normes légales. Votre examen a révélé que cinq stratégies de rétention partagent les mêmes paramètres, avec une seule étiquette de rétention appliquée, dont aucune ne répond correctement aux exigences légales.

Votre plan implique l’implémentation d’une nouvelle stratégie de rétention pour l’entreprise avec une période de rétention de cinq ans. Une fois cette période écoulée, les données peuvent être conservées, mais leur suppression n’est pas obligatoire. Cet ajustement répond aux exigences légales pour les périodes de rétention minimales et réduit la surcharge des données.

1. Connectez-vous au portail de conformité Microsoft Purview **`https://purview.microsoft.com/`** en tant qu’Allan Deyoung à l’aide du compte **Administrateur MOD**.
1. Si vous êtes invité à configurer une authentification multifacteur, suivez les instructions.
1. Vous accédez à la nouvelle page d’accueil du portail Microsoft Purview. Cochez la case en regard de **J’accepte les conditions de divulgation de flux de données et les déclarations de confidentialité**, puis sélectionnez **Démarrer**.
1. Dans le volet de navigation de gauche, sélectionnez **Solutions**, puis **Gestion du cycle de vie des données**. Vous pouvez également sélectionner la vignette **Afficher toutes les solutions** dans la fenêtre principale, puis sélectionner la vignette ***Gestion du cycle de vie des données** sous Gouvernance des données.

1. Dans le volet **Gestion du cycle de vie des données**, développez **Stratégies** et sélectionnez **Stratégies de rétention**.
1. Sur la page **Stratégies de rétention**, sélectionnez **+ Nouvelle stratégie de rétention**.
1. Sur la page **Nommer votre stratégie de rétention**, entrez les informations suivantes :
    - **Nom :** **`General retention policy`**
    - **Description** : **`This policy is the default retention policy for the entire organization. All data must be retained for at least 5 years.`**
1. Cliquez sur **Suivant**.
1. Sur la page **Étendue de la stratégie**, sélectionnez **Suivant**.
1. Sur la page **Choisir le type de stratégie de rétention à créer**, sélectionnez **Statique**, puis **Suivant**.
1. Sur la page **Choisir où appliquer cette stratégie**, activez les éléments suivants :

    - Les boîtes aux lettres Exchange
    - Sites classiques et de communication SharePoint
    - Comptes OneDrive
    - Boîtes aux lettres de groupe et sites Microsoft 365

1. Cliquez sur **Suivant**.
1. Sur la page **Décider si vous voulez conserver du contenu, le supprimer ou les deux**, définissez les paramètres suivants :

    - Conserver les éléments pendant une période spécifique : **5 ans**
    - Démarrer la période de rétention en fonction de : **Quand les éléments ont été créés**
    - À la fin de la période de rétention : **Ne rien faire**

1. Cliquez sur **Suivant**.
1. Sur la page **Vérifier et terminer**, sélectionnez **Envoyer**, puis **Terminé**.

Vous avez créé une stratégie de rétention. Vous pouvez maintenant supprimer toutes les stratégies de rétention restantes, car elles ne répondent pas aux exigences de l’entreprise.

### Tâche 3 : créer une étiquette de rétention

Pour respecter les réglementations allemandes, vous allez maintenant créer une étiquette de rétention avec une période de rétention de 10 ans et l’appliquer automatiquement à tous les documents qui contiennent des données financières allemandes.

1. Vous devez toujours être connecté à la solution **Gestion du cycle de vie des données** dans le portail Microsoft Purview.  Si ce n’est pas le cas, accédez à **`https://purview.microsoft.com/`** > **Solutions** > **Gestion du cycle de vie de vie des données**.
1. Dans le volet **Gestion du cycle de vie des données**, sélectionnez **Étiquettes de rétention**.
1. Sur la page **Étiquettes**, sélectionnez **+ Créer une étiquette**.
1. Sur la page **Nommer votre étiquette de rétention**, entrez les informations suivantes :

    - Nom : **`German financial data`**
    - Description pour les utilisateurs : **`This label retains all German financial data for 10 years.`**
    - Description pour les administrateurs : **`The label retains all financial data for 10 years and it is automatically applied.`**

1. Cliquez sur **Suivant**.
1. Sur la page **Définir les paramètres d’étiquette**, sélectionnez **Appliquer les actions après une période spécifique**, puis **Suivant**.
1. Sur la page **Définir la période**, entrez les informations suivantes :

    - Quelle est la durée de la période ? : **10 ans**
    - Quand la période doit-elle commencer ? : **Quand des éléments ont été créés**

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir ce qui se passe à la fin de la période**, sélectionnez **Supprimer automatiquement les éléments**. Sélectionnez **Suivant**.
1. Sur la page **Vérifier et terminer**, sélectionnez **Créer une étiquette**.
1. Sur la page **Votre étiquette de rétention a été créée**, sélectionnez **Appliquer automatiquement cette étiquette à un type spécifique de contenu**, puis **Terminé**.
1. Sur la page **Démarrer**, entrez les informations suivantes :

    - Nom : **`Automatically retain all German financial data for 10 years`**
    - Descriptions : **`This policy auto-applies the label German financial data.`**

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir le type de contenu auquel vous voulez appliquer cette étiquette**, sélectionnez **Appliquer l’étiquette au contenu qui contient des informations sensibles**, puis cliquez sur **Suivant**.
1. Sur la page **Contenu contenant des informations confidentielles**, définissez le filtre sur **Allemagne**, sélectionnez **Financier**, puis **Données financières allemandes**, puis sélectionnez **Suivant**.
1. Dans la page **Définir le contenu qui contient des informations sensible**, laissez tous les paramètres existants (aucune modification) et sélectionnez **Suivant**.
1. Sur la page **Étendue de la stratégie**, sélectionnez **Suivant**.
1. Sur la page **Choisir le type de stratégie de rétention à créer**, sélectionnez **Statique**.
1. Sur la page **Choisir où appliquer automatiquement l’étiquette**, activez les emplacements suivants :

    - Les boîtes aux lettres Exchange
    - Sites classiques et de communication SharePoint
    - Comptes OneDrive
    - Boîtes aux lettres de groupe et sites Microsoft 365

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir une étiquette à appliquer automatiquement**, vérifiez que l’étiquette **Données financières allemandes** est bien affichée. Sinon, ajoutez-la à l’aide du bouton **+ Ajouter une étiquette**. Cliquez sur **Suivant**.
1. Sur la page **Décider de tester ou d’exécuter votre stratégie**, sélectionnez **Activer la stratégie**, puis **Suivant**.
1. Sur la page **Vérifier et terminer**, sélectionnez **Envoyer**, puis **Terminé**.

Vous avez créé et appliqué automatiquement une étiquette de rétention.
