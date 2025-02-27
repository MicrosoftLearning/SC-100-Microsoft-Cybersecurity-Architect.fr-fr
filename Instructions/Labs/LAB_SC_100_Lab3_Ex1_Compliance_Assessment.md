---
lab: 3
title: "Exercice\_1 - Évaluation de la conformité"
---

# Labo 3 - Exercice 1 - Évaluation de la conformité

Contoso Ltd. s’étend en Europe pour augmenter les ventes, mais rencontre des difficultés à satisfaire les demandes de sécurité informatique des clients. Les clients souhaitent que Contoso maintienne un environnement sécurisé qui permette une collaboration sûre et minimise le risque de fuites de données et de compromission des ressources de l’entreprise. Beaucoup de clients exigent une preuve attestant que les processus opérationnels informatiques sont bien établis et que le cadre de sécurité est solide, ce qui prend souvent la forme d’une certification ISO-27001. Pour répondre à cette demande, Contoso a décidé de faire appel à un cabinet d’audit externe pour réaliser l’audit ISO-27001 et obtenir la certification. Pour cela, il est nécessaire d’évaluer la situation actuelle de l’organisation et d’élaborer un plan d’action pour répondre aux exigences de la norme ISO-27001. En tant qu’architecte de la cybersécurité de l’entreprise, vous êtes chargé d’identifier les lacunes existantes et d’affecter des tâches spécifiques aux personnes de l’organisation pour les combler.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour relever les défis auxquels Contoso Ltd est confronté.

### Approche de conception

Pour traiter efficacement la question décrite, il est essentiel de bien comprendre la norme ISO 27001. Il est essentiel d’évaluer la situation de Contoso par rapport aux normes ISO 27001 et de mettre en évidence les éventuelles incohérences pour les analyser. Compte tenu de la complexité de l’environnement M365 et de la réglementation 27001, ce processus peut prendre beaucoup de temps. Heureusement, l’évaluation du Gestionnaire de conformité Microsoft permet de simplifier cette analyse.

Les évaluations du Gestionnaire de conformité Microsoft sont des regroupements de contrôles tirés de réglementations, de normes ou de stratégies spécifiques. Ils vous aident à vous assurer que votre organisation répond aux exigences de diverses normes, réglementations ou lois. Par exemple, en réalisant toutes les actions d’une évaluation, vous pouvez aligner vos paramètres Microsoft 365 sur les exigences de la norme ISO 27001. Les évaluations englobent plusieurs composants et fournissent des modèles pour plus de 360 réglementations, avec les contrôles et les étapes nécessaires pour évaluer efficacement votre conformité. 

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Comparaison de l’environnement M365 avec les réglementations ISO 27001|Gestionnaire de conformité Microsoft Purview|Créer une évaluation|
|Créer un plan d’action|Gestionnaire de conformité Microsoft Purview|Affecter des tâches à un ingénieur technique|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : effectuer une évaluation ISO-27001

La première étape consiste à analyser l’environnement actuel de l’entreprise. Vous effectuez une évaluation de la conformité afin de déterminer dans quelle mesure l’environnement de Contoso est conforme à la norme ISO-27001.

1. Connectez-vous au portail de conformité Microsoft Purview **https://compliance.microsoft.com/** en tant qu’Allan Deyoung à l’aide de son compte **Administrateur MOD**.
2. Il vous sera demandé de configurer l’authentification multifacteur, suivez les instructions.
3. Dans le volet de navigation de gauche du portail de conformité Microsoft Purview, sélectionnez **Gestionnaire de conformité**.
4. Sur la page **Gestionnaire de conformité**, sélectionnez **Évaluation**.
5. Sur la page **Gestionnaire de conformité \| Évaluation**, sélectionnez **+ Ajouter une évaluation**.
6. Sur la page **Baser votre évaluation sur une réglementation**, sélectionnez **Sélectionner une règlementation**.
7. Dans la zone de texte de recherche, entrez **ISO-27001:2022**, sélectionnez la règlementation, sélectionnez **Enregistrer**, puis **Suivant**.
8. Sur la page **Ajouter un nom et un groupe**, dans la zone de texte **Nom de l’évaluation**, entrez **Évaluation d’audit ISO-27001**, puis sélectionnez **Suivant**.
9. Sur la page **Sélectionner des services**, sélectionnez **Sélectionner des services**, puis **Microsoft 365**, puis **Ajouter**, et enfin **Suivant**
10. Terminez la configuration et créez l’évaluation.

Vous avez créé une évaluation basée sur ISO-27001.

### Tâche 2 : affecter des tâches à un ingénieur technique

Les résultats de l’évaluation vous indiquent les différents domaines et actions qui sont essentiels pour se conformer à la norme ISO-27011. Vous allez examiner les actions d’amélioration et affecter une tâche à un ingénieur technique.

1. Vous devriez toujours être connecté au portail de conformité Microsoft Purview **https://compliance.microsoft.com/**.
2. Dans le volet de navigation de gauche du portail de conformité Microsoft Purview, sélectionnez **Gestionnaire de conformité**.
3. Sur la page **Gestionnaire de conformité**, sélectionnez l’évaluation **ISO/IEC-27001:2022** que vous avez créée.
4. Sur la page d’évaluation, sélectionnez le panneau **Vos actions d’amélioration**.
5. Définissez le filtre de **Famille de contrôles** sur **Contrôles physiques**.
6. Sélectionnez toutes les actions d’amélioration affichées, puis **Affecter à l’utilisateur**.
7. Sur la nouvelle page **Affecter des actions d’amélioration**, dans la zone de texte de recherche, entrez **Nestor Wilke**.
8. Sélectionnez l’utilisateur et cliquez sur **Affecter**.

Vous avez réussi à consulter et affecter une action d’amélioration à un ingénieur technique

### Tâche 3 : fournir l’accès à un ingénieur technique pour les actions d’amélioration.

Les utilisateurs ont besoin d’un accès pour afficher les tâches qui leur sont affectées. Vous allez accorder à Nestor Wilke un accès à l’évaluation.

1. Vous devriez toujours être connecté au portail de conformité Microsoft Purview **https://compliance.microsoft.com/**.
2. Dans le volet de navigation de gauche du portail de conformité Microsoft Purview, sélectionnez **Gestionnaire de conformité**.
3. Sur la page **Gestionnaire de conformité**, sélectionnez le volet **Évaluation**, puis l’évaluation **Évaluation d’audit ISO-27001**.
4. En haut à droite de la page **Évaluation ISO/IEC 27001**, sélectionnez **Gérer l’accès utilisateur**.
5. Sur la nouvelle page **Gérer l’accès utilisateur**, sélectionnez **Évaluateur**, puis **Ajouter des évaluateurs**.
6. Dans la zone de texte **Rechercher des utilisateurs**, entrez **Nestor Wilke**.
7. Sélectionnez l’utilisateur, puis **Enregistrer**.

Vous avez accordé à Nestor Wilke l’accès à l’évaluation.
