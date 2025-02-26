# Évaluation de la conformité

## Présentation du scénario de labo

Vous êtes Allan Deyoung, membre du service informatique de Contoso Ltd. Vous avez récemment été transféré à la division Sécurité informatique. Votre nouveau rôle consiste à évaluer si Contoso est préparée à la Confiance Zéro et à élaborer un plan d’action pour établir une initiative de Confiance Zéro conformément aux piliers de la Confiance Zéro. Contoso est une grande société multinationale avec une présence mondiale dans plusieurs industries. L’entreprise a une grande empreinte cloud et une infrastructure hybride. Le centre des opérations de sécurité (SOC) de Contoso est chargé de surveiller et de répondre aux incidents de sécurité au sein de l’entreprise. Il compte des analystes sécurité, des ingénieurs sécurité et des ingénieurs réseau. Il utilise Microsoft Sentinel comme solution de gestion des informations et des événements de sécurité (SIEM). Il utilise un espace de travail Log Analytics pour collecter et analyser les journaux de sécurité de l’ensemble de l’entreprise.

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

1. Connectez-vous au portail de conformité Microsoft Purview **`https://purview.microsoft.com/`** en tant qu’Allan Deyoung à l’aide du compte **Administrateur MOD**.
1. Si vous êtes invité à configurer une authentification multifacteur, suivez les instructions.
1. Vous accédez à la nouvelle page d’accueil du portail Microsoft Purview. Cochez la case en regard de **J’accepte les conditions de divulgation de flux de données et les déclarations de confidentialité**, puis sélectionnez **Démarrer**.
1. Dans le volet de navigation de gauche, sélectionnez **Solutions**, puis **Gestionnaire de conformité**. Vous pouvez également sélectionner la vignette **Afficher toutes les solutions** dans la fenêtre principale, puis sélectionner la vignette **Gestionnaire de conformité** sous Risque et conformité.
1. Dans le panneau **Gestionnaire de conformité** à gauche, sélectionnez **Évaluations**.
1. Dans la fenêtre **Évaluations**, sélectionnez **+ Ajouter une évaluation**.
1. Dans la fenêtre **Baser votre évaluation sur un réglement**, sélectionnez **Sélectionner un règlement**.
1. Dans la zone de recherche, entrez **`ISO/IEC 27001:2022`**, sélectionnez le règlement puis cliquez sur **Enregistrer** et sur **Suivant.**
1. Sur la page **Ajouter un nom et un groupe**, dans la zone de texte **Nom de l’évaluation**, entrez **`ISO-27001 Audit assessment`**. Laissez le paramètre **Groupe d’évaluation** sur **Utiliser le groupe existant** avec le **Groupe par défaut**, puis sélectionnez **Suivant**.
1. La page **Sélectionner des services** devrait déjà afficher le service **Microsoft 365**.  Si ce n’est pas le cas, sélectionnez **Sélectionner des services**, puis sélectionnez **Microsoft 365** et cliquez sur **Ajouter**. Cliquez sur **Suivant**.
1. Sur la page **Vérifier et terminer**, sélectionnez **Créer l’évaluation**. Une fois l’évaluation créée au bout de quelques secondes, sélectionnez **Terminé**.
1. Vous devez maintenant être sur la page **Évaluation de l’audit ISO-27001** qui vient d‘’être créée.
1. Laissez cet onglet ouvert pour la tâche suivante.

Vous avez créé une évaluation basée sur ISO-27001.

### Tâche 2 : affecter des tâches à un ingénieur technique

Les résultats de l’évaluation vous indiquent les différents domaines et actions qui sont essentiels pour se conformer à la norme ISO-27011. Vous allez examiner les actions d’amélioration et affecter une tâche à un ingénieur technique.

1. Vous devez toujours être sur la page d’évaluation que vous venez de créer, **Évaluation d’audit ISO-27001**.  Si ce n’est pas le cas, accédez au portail Microsoft Purview **`https://purview.microsoft.com/`**, puis sélectionnez **Solutions** > **Gestionnaire de conformité** > **Évaluations** > **Évaluation d’audit ISO-27001**
1. Sur la page **Évaluation d’audit ISO-27001**, sélectionnez **Vos actions d’amélioration**.
1. Définissez le filtre de **Famille de contrôles** sur **Contrôles physiques**.
1. Sélectionnez la zone en regard de **Action d’amélioration** pour sélectionner toutes les actions d’amélioration affichées, puis sélectionnez **Affecter à l’utilisateur** (au-dessus des options de filtres).
1. Dans la nouvelle fenêtre **Affecter des actions d’amélioration**, dans la zone de recherche, entrez **`Nestor`** et appuyez sur Entrée.
1. Sélectionnez l’utilisateur et cliquez sur **Affecter**.
1. Gardez l’onglet ouvert pour la prochaine tâche.

Vous avez réussi à consulter et affecter une action d’amélioration à un ingénieur technique

### Tâche 3 : fournir un accès à un ingénieur technique pour les actions d’amélioration

Les utilisateurs ont besoin d’un accès pour afficher les tâches qui leur sont affectées. Vous allez accorder à Nestor Wilke un accès à l’évaluation.

1. Vous devez être dans l’onglet **Vos actions d’amélioration** de la page **Évaluation de l’audit ISO-27001**.  Si ce n’est pas le cas, accédez au portail Microsoft Purview **`https://purview.microsoft.com/`**, puis sélectionnez **Solutions** > **Gestionnaire de conformité** > **Évaluations** > **Évaluation d’audit ISO-27001** > **Vos actions d’amélioration**.
1. Dans le coin supérieur droit de la page **ISO/IEC 27001 :Évaluation**, sélectionnez **Gérer l’accès des utilisateurs**.
1. Dans la nouvelle fenêtre **Gérer l’accès des utilisateurs**, sélectionnez l’onglet **Évaluateur** et cliquez sur **Ajouter des évaluateurs**.
1. Dans la zone de texte **Rechercher des utilisateurs**, entrez **`Nestor`** puis appuyez sur Entrée.
1. Sélectionnez l’utilisateur, cliquez sur **Appliquer**, puis sélectionnez **Enregistrer**.
1. Vous avez réussi à accorder à Nestor Wilke le rôle d’évaluateur pour cette évaluation.
1. Vous pouvez maintenant quitter le portail Microsoft Purview en fermant l’onglet du navigateur.

Vous avez réussi à accorder à Nestor Wilke le rôle d’évaluateur pour cette évaluation.
