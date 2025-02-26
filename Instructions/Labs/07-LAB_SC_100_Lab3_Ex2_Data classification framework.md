# Cadre de classification des données

On vous a confié la tâche de structurer la classification des données pour Contoso Ltd. afin de préparer l’audit ISO-27001:2022. L’objectif est d’établir un cadre solide qui est essentiel pour assurer une protection efficace contre les fuites, les suppressions et les pertes de données. Votre rôle implique l’intégration d’un nouveau système d’ID pour les projets de construction au sein de l’entreprise. Pour respecter les réglementations gouvernementales, tous les documents contenant un certain ID de projet doivent être conservés pendant 5 ans.

Vous avez reçu les exemples suivants pour classifier les ID de projet :

|ID Projet|
|----|
|PAR-1023-DA|
|BER-0822-AB|
|Rom-0419-bm|
|sTr*1223-Se|
|BaR#0418-ag|
|dui0522-in|

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour résoudre les problèmes auxquels Contoso Ltd est confronté.

### Approche de conception

L’introduction d’un nouvel identifiant de projet implique la création d’un type d’information sensible (SIT) correspondant. Pour cela, il est nécessaire de développer un modèle personnalisé incorporant une expression régulière. Par la suite, ce SIT peut être utilisé pour concevoir une étiquette de rétention et une stratégie d’étiquetage automatique associée.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Identifier les documents contenant des ID de projet|Protection des informations Microsoft Purview|Créer un type d’informations sensibles personnalisé|
|Respecter la réglementation gouvernementale pour conserver les données pendant 5 ans| Gestion de cycle de vie des données Microsoft Purview|Déployer une stratégie de rétention|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : créer un type d’informations sensibles personnalisé

Vous allez créer un type d’informations sensibles personnalisé pour détecter les documents qui contiennent des ID de projet.

1. Connectez-vous au portail de conformité Microsoft Purview **`https://purview.microsoft.com/`** en tant qu’Allan Deyoung à l’aide du compte **Administrateur MOD**.
1. Si vous êtes invité à configurer une authentification multifacteur, suivez les instructions.
1. Vous accédez à la nouvelle page d’accueil du portail Microsoft Purview. Cochez la case en regard de **J’accepte les conditions de divulgation de flux de données et les déclarations de confidentialité**, puis sélectionnez **Démarrer**.
1. Dans le volet de navigation de gauche, sélectionnez **Solutions**, puis **Protection des données**. Vous pouvez également sélectionner la vignette **Afficher toutes les solutions** dans la fenêtre principale, puis sélectionner la vignette **Protection des données** répertoriée sous Sécurité des données.
1. Développez **Classifieurs**, puis sélectionnez **Types d’informations sensibles**.
1. Sur la page **Types d’informations sensibles**, sélectionnez **Créer un type d’informations sensibles**.
1. Sur la page **Nommer votre type d’informations sensibles**, saisissez les informations suivantes :
    - Nom : **`Project Identification Number`**
    - Description : **`Identifies project identification number`**
1. Cliquez sur **Suivant**.
1. Dans la page **Définir des modèles pour ce type d’informations sensibles**, sélectionnez **Créer un modèle**.
1. Sur la page **Nouveau modèle**, sélectionnez **Ajouter un élément principal**, puis **Expression régulière**.
1. Sur la page **Ajouter une expression régulière** dans la zone de texte **ID**, tapez **`ProjectID`**.
1. Dans la zone de texte **Expression régulière**, entrez l’expression suivante :

    **`[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}`**

    >[!NOTE] L’expression régulière fournie est conçue pour identifier une séquence caractérisée par trois lettres, suivie de caractères facultatifs non signifiants, puis de quatre chiffres, suivis une fois de plus par des caractères facultatifs non signifiants et se terminant par deux lettres. La présence de caractères non signifiants est facultative et le modèle général doit correspondre à un format ou à une structure spécifique au sein des données.

1. Sous la zone de texte Expression régulière, sélectionnez **Correspondance de chaîne**, puis **Terminé**.
1. Dans la fenêtre **Nouveau modèle**, sous **Niveau de confiance**, sélectionnez **Confiance élevée**, puis cliquez sur **Créer** et sur **Suivant**.
1. Sur la page **Choisir le niveau de confiance recommandé à afficher dans les stratégies de conformité**, laissez la valeur **Niveau de confiance élevé**, puis sélectionnez **Suivant**.
1. Sous **Vérifier les paramètres et terminer**, vérifiez les paramètres, sélectionnez **Créer**, et une fois la stratégie créée, sélectionnez **Terminé**.

Vous avez créé un nouveau type d’informations sensibles pour identifier les ID de projet.

### Tâche 2 : créer une étiquette de rétention

Vous allez créer une étiquette de rétention pour conserver tous les documents liés aux projets de construction pendant 5 ans.

1. Vous devez toujours être connecté au portail Microsoft Purview **https://purview.microsoft.com/**.
1. Dans le volet de navigation de gauche, sélectionnez **Solutions**, puis **Gestion du cycle de vie des données**.
1. Sélectionnez **Étiquettes de rétention**.
1. Sur la page **Étiquettes**, sélectionnez **Créer une étiquette**.
1. Sur la page **Nommer votre étiquette de rétention**, entrez les informations suivantes :

    - Nom : **`Retention of Construction Project Documentation`**
    - Description pour les utilisateurs : **`The construction project documentation Retention Policy dictates the retention of all project-related documents for five years following project completion.`**
    - Description pour les administrateurs : **`This label is applied to retain construction project documents for a period of five years, and it is utilized in conjunction with auto-labeling.`**

1. Sélectionnez **Suivant**.
1. Sur la page **Définir les paramètres d’étiquette**, sélectionnez **Conserver les éléments indéfiniment ou pendant une période spécifique**, puis sélectionnez **Suivant**.
1. Sur la page **Définir la période de rétention**, entrez les informations suivantes :

    - Conserver les éléments pendant : **5 ans**
    - Démarrer la période de rétention en fonction de : **Quand les éléments ont été créés**

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir ce qui se passe après la période de rétention**, sélectionnez **Désactiver les paramètres de rétention**, puis **Suivant**.
1. Sur la page **Vérifier et terminer**, passez en revue les paramètres, puis sélectionnez **Créer l’étiquette**.
1. La page **Votre étiquette de rétention est créée** contient plusieurs options.  Sélectionnez **Ne rien faire**, puis cliquez sur **Terminé**.  Dans la tâche suivante, vous allez créer la stratégie d’application automatique. En sélectionnant Appliquer automatiquement cette étiquette à un type de contenu spécifique, vous suivez les étapes de la tâche suivante, qui commence à l’étape 4.

1. Laissez l’onglet du navigateur ouvert pour la prochaine tâche.

Vous avez créé une étiquette de rétention avec une période de rétention de 5 ans.

### Tâche 3 : appliquer automatiquement l’étiquette de rétention

Vous allez utiliser le type d’informations sensibles que vous avez créé dans cet exercice pour appliquer automatiquement l’étiquette de rétention.

1. Vous devez toujours être connecté à la solution de gestion du cycle de vie des données dans le portail Microsoft Purview.  Si ce n’est pas le cas, accédez à **`https://purview.microsoft.com/`** > **Solutions** > **Gestion du cycle de vie de vie des données**.
1. Dans le volet **Gestion du cycle de vie des données**, sélectionnez **Stratégies d’étiquette**.
1. Sur le panneau **Stratégies d’étiquette**, sélectionnez **Appliquer automatiquement une étiquette**.
1. Sur la page **C’est parti**, entrez les informations suivantes :

    - Nom : **`Label documents related to construction projects`**
    - Description : **`This policy automatically enforces the "Construction Project Documentation Retention" policy on any document pertaining to construction projects.`**

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir le type de contenu auquel vous voulez appliquer cette étiquette**, sélectionnez **Appliquer l’étiquette au contenu qui contient des informations sensibles**, puis **Suivant**.
1. Sur la page **Contenu qui contient des informations sensibles**, sélectionnez **Personnalisé**, puis **Stratégie personnalisée** et **Suivant**.

1. Sous **Définir le contenu qui contient des informations sensibles**, spécifiez les paramètres suivants :
    - Nom du groupe : **`Project ID lookup`**
    - Sous Types d’informations sensibles, sélectionnez **Ajouter** puis cliquez sur **Créer des types d’informations sensibles**.  
    - Sur la page Types d’informations sensibles, dans le champ de recherche, entrez le nom de l’étiquette que vous avez créée **`Project Identification number`** et appuyez sur Retour.  Sélectionnez **Numéro d’identification du projet**, puis cliquez sur **Ajouter**.
    - Laissez le niveau de confiance sur **Confiance élevée**.
    - Laissez le nombre d’instances sur **1 à indéfini**.
    - Sélectionnez **Suivant**.
1. Dans la page **Étendue de stratégie**, laissez le paramètre Unités d’administration sur **Répertoire complet**, puis sélectionnez **Suivant**.
1. Sur la page **Choisir le type de stratégie de rétention à créer**, sélectionnez **Statique**, puis cliquez sur **Suivant**.
1. Sous **Choisir où appliquer automatiquement l’étiquette**, vérifiez que l’état est **activé** pour tous les emplacements disponibles, puis sélectionnez **Suivant**.
1. Sous **Choisir une étiquette à appliquer automatiquement**, sélectionnez **Ajouter une étiquette**, puis sélectionnez l’étiquette **Rétention de la documentation du projet de construction** que vous avez créée à la tâche précédente. Sélectionnez **Ajouter**, puis **Suivant**.
1. Sous **Décider de tester ou d’exécuter votre stratégie**, sélectionnez **Activer la stratégie**, puis **Suivant**.
1. Sur la page **Vérifier et terminer**, vérifiez vos paramètres, puis sélectionnez **Envoyer** et **Terminé**.

Vous avez correctement publié et appliqué automatiquement l’étiquette de rétention à tous les documents qui contiennent des ID de projet.
