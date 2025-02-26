---
lab: 3
title: "Exercice\_2 - Cadre de classification des données"
---


# Labo 3 - Exercice 2 - Cadre de classification des données

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

1. Connectez-vous au portail de conformité Microsoft Purview **https://compliance.microsoft.com/** en tant qu’Allan Deyoung à l’aide de son compte **Administrateur MOD**.
1. Dans le portail de conformité Microsoft Purview, développez **Classification des données** dans le volet de navigation de gauche, puis sélectionnez **Classifieurs**.
3. Sur la page **Classifieurs**, sélectionnez **Types d’informations sensibles** > **Créer un type d’informations sensibles**.
4. Sur la page **Nommer votre type d’informations sensibles**, saisissez les informations suivantes :
    - **Nom** : numéro d’identification du projet
    - **Description** : identifie le numéro d’identification du projet
1. Cliquez sur **Suivant**.
1. Dans la page **Définir des modèles pour ce type d’informations sensibles**, sélectionnez **Créer un modèle**.
1. Sur la page **Nouveau modèle**, sélectionnez **Ajouter un élément principal**, puis **Expression régulière**.
1. Sur la page **Ajouter une expression régulière** dans la zone de texte **ID**, tapez **ProjectID**.
1. Dans la zone de texte **Expression régulière**, entrez l’expression suivante :

```
[a-zA-Z]{3}(\W)?[\d]{4}(\W)?[a-zA-Z]{2}
```

> [!NOTE] L’expression régulière fournie est conçue pour identifier une séquence caractérisée par trois lettres, suivie de caractères facultatifs non signifiants, puis de quatre chiffres, suivis une fois de plus par des caractères facultatifs non signifiants et se terminant par deux lettres. La présence de caractères non signifiants est facultative et le modèle général doit correspondre à un format ou à une structure spécifique au sein des données.

1. Sélectionnez **Correspondance de chaîne** pour les **expressions régulières**, puis sélectionnez **Terminé**.
1. Dans la partie supérieure, sélectionnez **Confiance élevée** sous **Niveau de confiance**, puis sélectionnez **Créer**.
1. Terminez la configuration et créez le type d’informations sensibles.

Vous avez créé un nouveau type d’informations sensibles pour identifier les ID de projet.

### Tâche 2 : créer une étiquette de rétention

Vous allez créer une étiquette de rétention pour conserver tous les documents liés aux projets de construction pendant 5 ans.

1. Vous devriez toujours être connecté au portail de conformité Microsoft Purview **https://compliance.microsoft.com/**.
1. Dans le portail de conformité Microsoft Purview, dans le volet de navigation de gauche, développez **Gestion du cycle de vie des données** et sélectionnez **Microsoft 365**.
1. Sur la page **Gestion du cycle de vie des données**, sélectionnez le panneau **Étiquettes**.
1. Dans le panneau **Étiquettes**, sélectionnez **+ Créer une étiquette**.
1. Sur la page **Nommer votre stratégie de rétention**, entrez les informations suivantes :

    - **Nom** : rétention de la documentation des projets de construction
    - **Description pour les utilisateurs et les utilisatrices** : la stratégie de rétention de la documentation du projet de construction détermine la méthode de conservation de tous les documents liés au projet pendant cinq ans après l’achèvement du projet
    - **Description pour les administrateurs** : cette étiquette est appliquée pour conserver les documents des projets de construction pendant une période de cinq ans, et elle est utilisée conjointement avec l’étiquetage automatique.

1. Sélectionnez **Suivant**.
1. Sur la page **Définir les paramètres d’étiquette**, sélectionnez **Conserver les éléments indéfiniment ou pendant une période spécifique**, puis sélectionnez **Suivant**.
1. Sur la page **Définir la période de rétention**, entrez les informations suivantes :

    - **Conserver les éléments pour **: 5 ans
    - **Démarrer la période de rétention en fonction de** : Quand les éléments ont été créés

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir ce qui se passe après la période de rétention**, sélectionnez **Désactiver les paramètres de rétention**.
1. Terminez la configuration et créez l’étiquette de rétention sans la publier.

Vous avez créé une étiquette de rétention avec une période de rétention de 5 ans.

### Tâche 3 : appliquer automatiquement l’étiquette de rétention

Vous allez utiliser le type d’informations sensibles que vous avez créé dans cet exercice pour appliquer automatiquement l’étiquette de rétention.

1. Vous devriez toujours être connecté au portail de conformité Microsoft Purview **https://compliance.microsoft.com/**.
1. Dans le portail de conformité Microsoft Purview, développez **Gestion du cycle de vie des données** et sélectionnez **Microsoft 365**.
1. Sur la page **Gestion du cycle de vie des données**, sélectionnez le panneau **Stratégies d’étiquette**.
1. Sur le panneau **Stratégies d’étiquette**, sélectionnez **Appliquer automatiquement une étiquette**.
1. Sur la page **C’est parti**, entrez les informations suivantes :

    - **Nom** : étiqueter les documents liés aux projets de construction
    - **Description** : cette stratégie applique automatiquement la stratégie « Rétention de la documentation des projets de construction » à tout document en rapport avec des projets de construction.

1. Cliquez sur **Suivant**.
1. Sur la page **Choisir le type de contenu auquel vous voulez appliquer cette étiquette**, sélectionnez **Appliquer l’étiquette au contenu qui contient des informations sensibles**, puis **Suivant**.
1. Sur la page **Contenu qui contient des informations sensibles**, sélectionnez **Personnalisé**, puis **Stratégie personnalisée** et **Suivant**.
Sous **Définir le contenu qui contient des informations sensibles**, ajoutez le type d’informations sensibles personnalisé que vous avez créé **Numéro d’identification du projet**. Spécifiez ensuite les paramètres suivants :

    - **Nom du groupe** : recherche d’ID de projet
    - **Niveau de confiance** : confiance élevée
    - **Nombre d’instances** : 1 à indéfini

1. Sélectionnez **Suivant**.
1. Sur la page **Étendue de la stratégie**, sélectionnez **Suivant**.
1. Sur la page **Choisir le type de stratégie de rétention à créer**, sélectionnez **Statique**, puis cliquez sur **Suivant**.
1. Appliquez l’étiquette à tous les emplacements disponibles.
1. Sous **Choisir une étiquette à appliquer automatiquement**, sélectionnez **Ajouter une étiquette**, puis sélectionnez l’étiquette **Rétention de la documentation du projet de construction** que vous avez créée dans la tâche 2 et cliquez sur **Ajouter**.
1. Activez et terminez la configuration pour créer la stratégie d’étiquetage automatique.

Vous avez correctement publié et appliqué automatiquement l’étiquette de rétention à tous les documents qui contiennent des ID de projet.