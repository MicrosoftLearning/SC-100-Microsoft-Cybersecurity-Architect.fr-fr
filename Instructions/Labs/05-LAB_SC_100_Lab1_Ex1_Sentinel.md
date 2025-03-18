# Centre des opérations de sécurité

## Vue d’ensemble de l’exercice

Contoso dispose d’un centre des opérations de sécurité (SOC) qui surveille et répond aux incidents de sécurité au sein de l’entreprise. Il compte des analystes sécurité, des ingénieurs sécurité et des ingénieurs réseau. Le SOC a décidé d’utiliser Microsoft Sentinel comme solution de gestion des informations et des événements de sécurité (SIEM). Pour collecter et analyser les journaux de sécurité de l’entreprise, le SOC dispose d’un espace de travail Log Analytics. Le SOC a besoin de sécuriser l’accès à l’espace de travail Log Analytics selon le principe du moindre privilège. Il existe deux rôles distincts au SOC, analyste de sécurité et ingénieur de sécurité, qui requièrent des niveaux d’autorisation différents. L’équipe réseau a besoin d’accéder uniquement aux journaux Cisco Umbrella.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept de surveillance et de réponse aux événements de sécurité avec des autorisations d’accès spécifiques pour le centre des opérations de sécurité de Contoso.

### Approche de conception

La première étape consiste à analyser les exigences en fonction du scénario, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Déployer une solution SIEM/SOAR
- Limiter l’accès à des rôles spécifiques du SOC
- Créer un tableau de bord avec des vues personnalisées pour les incidents et leurs alertes

Dans ce scénario, vous déployez la solution SIEM SOAR basée sur Microsoft Sentinel. Vous configurez le contrôle d’accès en fonction du rôle dans le contexte de l’espace de travail et vous limitez l’accès de l’équipe réseau à une seule table dans l’espace de travail Log Analytics. Les classeurs permettent aux analystes de sécurité et à l’équipe d’administration de visualiser les données de sécurité à l’aide d’affichages graphiques. Ils incluent un outil permettant de présenter et d’analyser des données dans un tableau de bord.

### Solution proposée

| Exigence | Solution | Plan d’action |
| ---- | ---- | ---- |
| Déployer une solution SIEM/SOAR | Microsoft Sentinel, espace de travail Log Analytics | Configurer l’espace de travail Log Analytics et déployer Microsoft Sentinel |
| Limiter l’accès à des rôles spécifiques du SOC | Espace de travail Log Analytics, contrôle d’accès en fonction du rôle (RBAC) | Configurer le RBAC pour l’espace de travail Log Analytics |
| Créer un tableau de bord avec des vues personnalisées pour les incidents et leurs alertes | Microsoft Sentinel, classeur | Créer un classeur avec une vue personnalisée des incidents et alertes actuels |

## Partie 2 : implémenter la solution (facultatif)

> [!NOTE]
> Pour cette partie du labo, la tâche consistant à créer un tableau de bord avec des vues personnalisées pour les incidents et leurs alertes (tâche 4 de cet exercice) ne fonctionne pas, car il n’existe aucune donnée sur laquelle effectuer cette tâche. Les étapes de la tâche 4 sont incluses uniquement à titre indicatif. L’exécution des étapes ne retourne aucune donnée.

### Tâche 1 : créer un espace de travail Log Analytics

Dans cette tâche, vous allez créer un espace de travail Log Analytics. Vous en avez besoin pour héberger toutes les données que Microsoft Sentinel doit ingérer et utiliser pour ses détections et analyses.

1. Connectez-vous à la machine virtuelle Client 1 (LON-SC1) en tant que compte **lon-sc1\admin** . Le mot de passe doit vous être fourni par votre fournisseur d’hébergement de labo.
2. Ouvrez **Microsoft Edge**, sélectionnez la barre d’adresse, accédez à **`https://portal.azure.com`** et connectez-vous au Portail Azure en tant qu’**utilisateur1-*******@LODSUATMCA.onmicrosoft.com** (où ****** est votre ID de locataire unique fourni par votre fournisseur d’hébergement de labo). Le mot de passe de l’utilisateur doit être fourni par votre fournisseur d’hébergement de labo.
3. Dans la boîte de dialogue Rester connecté ?, cochez la case Ne plus afficher, puis sélectionnez **Non**.
4. Fermez la boîte de dialogue d’enregistrement de mot de passe en bas en sélectionnant Jamais, pour ne pas enregistrer les informations d’identification des administrateurs généraux par défaut dans votre navigateur.
5. Dans l’écran Bienvenue dans Microsoft Azure, sélectionnez Annuler.
6. Sélectionnez **Créer une ressource** et cherchez **Espace de travail Log Analytics**
7. Cherchez la **vignette Espace de travail Log Analytics**, sélectionnez **Créer**.
8. Sur la page Créer un espace de travail Log Analytics, créez un **Groupe de ressources** et nommez-le **`rg_eastus_soc`**.
9. Dans les détails de l’instance, entrez le nom **`law-sentinel`** et sélectionnez la région **USA Est**.
10. Sélectionnez **Vérifier et créer**
11. Sélectionnez **Créer** pour démarrer le déploiement.

Vous avez créé l’espace de travail Log Analytics pour votre déploiement Sentinel.

### Tâche 2 : Créer Sentinel

Dans cette tâche, vous allez ajouter Sentinel à l’espace de travail Log Analytics créé et ajouter des journaux de démonstration. Comme le locataire de démonstration ne dispose actuellement pas de données dans l’espace de travail Log Analytics, vous importez des journaux de démonstration pour avoir une meilleure idée du fonctionnement de Sentinel.

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Dans la barre de recherche, dans la bannière bleue située en haut de la page, entrez **Microsoft Sentinel**, puis sélectionnez-le dans les résultats de la recherche répertoriés sous Services.
1. Sur la page **Microsoft Sentinel**, sélectionnez **Créer**.
1. Sur la page **Ajouter Microsoft Sentinel à un espace de travail**, l’espace de travail Log Analytics créé précédemment devrait apparaître.  Sélectionnez **law-sentinel**, puis **Ajouter**.
1. L’ajout de Sentinel à l’espace de travail peut prendre quelques minutes.  Une fois ajouté, la page **Microsoft Sentinel | Actualités et guides** s’affiche.  Un message vous informe que l’évaluation gratuite de Microsoft Sentinel est activée.  Sélectionnez **OK**.
1. Au centre de la page, sélectionnez **Accéder au hub de contenu**.  Le hub de contenu est l’endroit où vous allez télécharger des solutions. Explorez le hub de contenu à votre gré.

Vous avez correctement déployé Sentinel sur l’espace de travail Log Analytics. 

### Tâche 3 : configurer le RBAC

Vous devez sécuriser l’accès en fonction du moindre privilège. Vous allez créer des attributions de rôles pour les exigences de rôle spécifiques. Dans votre déploiement de production à venir, le centre de sécurité des opérations (SOC) comprendra deux rôles différents.
En outre, l’équipe réseau a besoin d’accéder aux journaux Cisco Umbrella. Vous devez vous assurer que l’équipe réseau ne peut accéder qu’à ces journaux.

#### Spécifications relatives aux autorisations

| Rôle | Autorisations |
|---|---|
| Analyste de sécurité | Afficher les données, incidents, classeurs et autres ressources Sentinel |
| | Affectation/abandon d’incidents. |
| Ingénieur Sécurité | Créer et modifier des classeurs et des règles d’analyse |
| | Installer et mettre à jour des solutions à partir du hub de contenu |
| Équipe réseau | Autorisations de lecture pour le groupe : **NOC** sur la table : **Cisco_Umbrella_dns_CL**|

---

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Dans la barre de recherche supérieure, recherchez **Groupes de ressource** et sélectionnez le groupe de ressources créé précédemment **rg_eastus_soc**.
1. Dans le volet de navigation gauche, sélectionnez **Contrôle d’accès (IAM)**.
1. Dans la liste déroulante, sélectionnez **Ajouter**, puis **Ajouter une attribution de rôle**.
1. Recherchez **`Microsoft Sentinel Responder`** et sélectionnez **Afficher** dans la colonne Détails.
1. Vérifier les autorisations correspondent aux exigences.
1. Fermez la fenêtre avec **X** dans le coin supérieur droit.
1. Cliquez sur **Suivant**.
1. Cliquez sur **+ Sélectionner des membres**.
1. Recherchez le groupe **`SOC Analysts`**, sélectionnez **Analystes SOC** dans les résultats de la recherche, cliquez sur **Sélectionner** et ajoutez l’attribution de rôle.
1. Sélectionnez **Examiner + Attribuer**.
1. Vous allez répéter ces étapes pour le rôle Collaborateur Sentinel. Dans la liste déroulante, sélectionnez **Ajouter**, puis **Ajouter une attribution de rôle**.
1. Recherchez **`Microsoft Sentinel Contributor`**, puis sélectionnez le rôle.
1. Cliquez sur **Suivant**.
1. Cliquez sur **+ Sélectionner des membres**.
1. Dans le panneau **Sélectionner des membres**, recherchez le groupe **Ingénieurs SOC**.  Dans les résultats de recherche, sélectionnez **Ingénieurs SOC** et appuyez sur **Sélectionner** pour ajouter l’attribution de rôle.
1. Sélectionner **Vérifier + attribuer** 2 fois
1. Sélectionnez l’onglet **Attributions de rôles** et vérifiez que les attributions de rôle sont définies.
1. Vous allez maintenant ajouter un rôle personnalisé. Sélectionnez **Ajouter**, puis **Ajouter un rôle personnalisé** dans le menu déroulant.
1. Nommez-le **`NOC-CiscoUmbrellaCL-Read`**.
1. Sous **Autorisations de base**, sélectionnez **Commencer à partir de zéro**.
1. Cliquez sur **Suivant**.
1. Sous l’onglet **Autorisations**, sélectionnez **Ajouter des autorisations**.
1. Cherchez **`Microsoft.OperationalInsights`** et sélectionnez la carte **Azure Log Analytics**.
1. Ajoutez les autorisations suivantes.
    - Microsoft.OperationalInsights/workspaces
        - Lire : obtenir un espace de travail
        - Autre : rechercher des données d’espace de travail

    - Microsoft.OperationalInsights/workspaces/analytics
        - Autre : Rechercher

    - Microsoft.OperationalInsights/workspaces/query
        - Lire : interroger les données dans un espace de travail

    - Microsoft.OperationalInsights/workspaces/tables/query
        - Lire : interroger des données de table d’un espace de travail

1. Sélectionnez **Vérifier + créer**.
1. Sélectionnez **Créer**, puis **OK**.
1. Dans la barre de recherche supérieure, recherchez **`Resource groups`** puis sélectionnez **rg_eastus_soc**.
1. Ouvrez l’espace de travail Log Analytics **law-sentinel**.
1. Dans le volet de navigation de gauche, développez **Paramètres**, puis sélectionnez **Tables**.
1. Recherchez **`Cisco_Umbrella_dns_CL`**.
1. Cliquez sur les points de suspension (...) puis sélectionnez **Contrôle d’accès (IAM)**.
1. Sélectionnez **Ajouter** > **Ajouter une attribution de rôle**.
1. Recherchez **`NOC-CiscoUmbrellaCL-Read`**, puis sélectionnez le rôle personnalisé.
1. Cliquez sur **Suivant**.
1. Sélectionnez **Sélectionner des membres**, cherchez **NOC**, sélectionnez-le dans les résultats de la recherche, puis cliquez sur **Sélectionner**
1. Sélectionner **Vérifier + attribuer** 2 fois

Vous avez créé le modèle d’accès basé sur les rôles pour l’équipe chargée des opérations de sécurité de Contoso, créé un rôle personnalisé pour l’équipe réseau et attribué le rôle sur la table spécifique de votre espace de travail Log Analytics.

### Tâche 4 : créer un classeur

> [!NOTE]
> Ces étapes sont incluses uniquement à titre indicatif. L’exécution des étapes ne retourne aucune donnée.

Dans cette tâche, vous allez créer un classeur pour obtenir un tableau de bord avec des vues personnalisées, les incidents actuels et leurs alertes.

1. Vous devez toujours être connecté au Portail Azure **https://portal.azure.com**.
1. Dans la barre de recherche supérieure, cherchez **`Microsoft Sentinel`** et ouvrez-le.
1. Sélectionnez **law-sentinel**.
1. Dans le volet de navigation de gauche, développez **Gestion des menaces**, puis sélectionnez **Classeurs**.
1. Sélectionnez **Ajouter un classeur**.
1. Sélectionnez **Modifier**.
1. Sélectionnez le premier bouton **Modifier** sur le côté droit.
1. Sélectionnez **Ajouter** > **Ajouter des paramètres**.
1. Sélectionnez **Ajouter un paramètre**, puis entrez les informations suivantes :
     - **Nom du paramètre :** TimeRange
     - **Type de paramètre :** sélecteur d’intervalle de temps.
1. Vérifiez les paramètres suivants :
     - **Obligatoire ?**
1. Cliquez sur **Enregistrer**.
1. Dans le menu déroulant **Intervalle de temps :** en bas à gauche, sélectionnez **7 derniers jours**.
1. Sélectionnez **Ajouter un paramètre**, puis entrez les informations suivantes :
     - **Nom du paramètre :** AlertSeverity
     - **Type de paramètre :** liste déroulante
1. Vérifiez les paramètres suivants :
     - **Obligatoire ?**
     - **Autoriser les sélections multiples**
     - **Masquer le paramètre en mode de lecture**
1. Sous **Requête de journal de l'espace de travail Log Analytics**, collez :

    ```KQL
    SecurityAlert
    | summarize Count = count() by AlertSeverity
    | order by Count desc, AlertSeverity
    | project Value = AlertSeverity, Label = strcat(AlertSeverity, ' - ', Count)
    ```

1. Dans le menu déroulant **Intervalle de temps**, sélectionnez **TimeRange**.
1. Faites défiler la page jusqu’à **Inclure dans la liste déroulante**, cochez **Tout** puis définissez **Élément sélectionné par défaut** sur **Tout**.
1. Cliquez sur **Enregistrer**.
1. Sélectionnez **Ajouter un paramètre**, puis entrez les informations suivantes :
     - **Nom du paramètre :** ProductName
     - **Type de paramètre :** liste déroulante
1. Vérifiez les paramètres suivants :
     - **Obligatoire ?**
     - **Autoriser les sélections multiples**
     - **Masquer le paramètre en mode de lecture**

1. Sous **Requête de journal de l'espace de travail Log Analytics**, collez :

    ```KQL
    SecurityAlert
    | summarize Count = count() by ProductName
    | order by Count desc, ProductName asc
    | project Value = ProductName, Label = strcat(ProductName, ' - ', Count)
    ```

1. Dans la liste déroulante **Intervalle de temps**, sélectionnez **TimeRange**.
1. Faites défiler la page jusqu’à **Inclure dans la liste déroulante**, cochez **Tout** puis définissez **Élément sélectionné par défaut** sur **Tout**.
1. Cliquez sur **Enregistrer**.
1. Sélectionnez **Ajouter**, puis **Ajouter une requête**.
1. Sous **Requête de journal de l'espace de travail Log Analytics**, collez :

    ```KQL
    SecurityIncident
    | where CreatedTime {TimeRange:value}
    | summarize arg_max(TimeGenerated,*) by tostring(IncidentNumber)
    | extend IncidentID = IncidentName
    | extend Alerts = extract("\\[(.*?)\\]", 1, tostring(AlertIds))
    | mv-expand AlertIds to typeof(string)
    | join
    (
        SecurityAlert
        | extend AlertEntities = parse_json(Entities)
        | mv-expand AlertEntities
    ) on $left.AlertIds == $right.SystemAlertId
    | summarize AlertCount=dcount(AlertIds) by IncidentNumber, Status, Severity, Title, Alerts, IncidentUrl, IncidentID
    | project IncidentNumber, IncidentID, Title, Severity, Status, AlertCount, Alerts, IncidentUrl
    | order by Severity
    ```

1. Dans la liste déroulante Intervalle de temps, sélectionnez **TimeRange**.
Vous allez configurer un contenu dynamique pour obtenir toutes les alertes pour l’incident sélectionné. Les alertes seront exportées et disponibles en dehors de cette requête.
1. Sélectionnez l’onglet **Paramètres avancés** en haut de la fenêtre **Requête de modification**.
1. Vérifiez les paramètres suivants :
    - **Lors de la sélection d’élément, exporter les paramètres** 
1. Sélectionnez **Ajouter un paramètre**, puis entrez les informations suivantes :
    - **Champ pour exporter :** Alertes
    - **Nom du paramètre :** Alertes
1. Cliquez sur **Enregistrer**.
1. Retournez à l’onglet **Paramètres**.
1. Sélectionnez **Run Query** (Exécuter la requête).
1. Sélectionnez **Paramètres de colonne**.
1. Sélectionnez **IncidentUrl**.
1. Définissez Convertisseur de colonne sur **Lien**.
1. Sous Paramètres de lien, définissez **Affichage à ouvrir** sur **URL**.
1. Sélectionnez **Enregistrer et fermer**.
1. Vous allez ensuite créer la vue des alertes en fonction de l’incident sélectionné.
1. Sélectionnez **+ Ajouter** en bas de la fenêtre **Modification d'élément de requête**. Sélectionnez **+ Ajouter une requête**.
1. Coller le KQL dans la requête de journal de l’espace de travail Log Analytics

    ```KQL
    SecurityAlert
    | where SystemAlertId in ({Alerts})
    | summarize by  DisplayName, StartTime, EndTime,  SystemAlertId
    | sort by EndTime desc
    ```

1. Dans la liste déroulante Intervalle de temps, sélectionnez **TimeRange**.
1. Sélectionnez **Modification terminée**.
1. Sélectionnez **Modification terminée** dans la barre supérieure de la fenêtre **Nouveau classeur**.
1. Sélectionnez un **Incident**.
1. Les alertes liées à l'incident s'affichent plus bas.
1. Enregistrez votre requête en cliquant sur l’icône Enregistrer.  
1. Dans la fenêtre **Enregistrer sous**, entrez un titre pour votre nouveau classeur, sélectionnez le groupe de ressources **rg_eastus_soc** dans la liste déroulante, puis sélectionnez **Enregistrer sous**.

Vous avez créé un tableau de bord avec des vues personnalisées pour les incidents et les alertes associées.
