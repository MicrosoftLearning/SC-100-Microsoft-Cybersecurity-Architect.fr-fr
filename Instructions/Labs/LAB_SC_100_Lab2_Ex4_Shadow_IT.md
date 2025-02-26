---
lab: 3
title: "Exercice\_4 - Informatique fantôme"
---


# Labo 2 - Exercice 4 - Informatique fantôme

L’infrastructure informatique de Contoso a évolué au cours des dernières décennies, fournissant diverses instances de serveur, applications et services. L’entreprise a récemment donné la priorité à la sécurisation de son environnement en mettant en œuvre la gestion des appareils, la gouvernance des données et la protection des identités et des applications au cours des deux dernières années. Cependant, le processus de restriction des utilisateurs aux seules applications spécifiques déployées par l’entreprise n’a pas encore été établi, ce qui permet aux utilisateurs d’installer des applications issues de diverses sources. En tant qu’architecte de la cybersécurité de l’organisation, vous devez avoir une vue d’ensemble de toutes les applications utilisées par les employés. Votre mesure de protection consiste à bloquer les applications non sécurisées dans votre environnement. 

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour relever les défis auxquels Contoso Ltd est confronté.

### Approche de conception

Dans le scénario donné, votre action initiale consiste à analyser et à découvrir toutes les applications actuellement utilisées par les employés. Les applications non autorisées installées par les utilisateurs peuvent présenter des risques de sécurité pour l’entreprise, d’où la nécessité d’identifier l’informatique fantôme. L’étape suivante consiste à éliminer les risques posés par ces applications dangereuses.

Defender for Cloud Apps est une solution de sécurité conçue pour résoudre les risques de l’informatique fantôme dans les environnements cloud. Elle aide les organisations à découvrir et à surveiller les applications cloud non autorisées utilisées par les employés, à évaluer leur état de sécurité et à appliquer des stratégies visant à garantir la conformité et à protéger les données. En offrant visibilité et contrôle sur l’informatique fantôme, Defender for Cloud Apps aide les organisations à atténuer les risques de sécurité associés à l’utilisation non autorisée du cloud et améliore ainsi la sécurité de leur environnement cloud.

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Découvrir l’informatique fantôme|Microsoft Defender for Cloud Apps|Examiner toutes les applications dans l’environnement de Contoso|
|Bloquer toutes les applications non sécurisées|Microsoft Defender for Cloud Apps|Marquer les applications non sécurisées comme non approuvées|

## Partie 2 : implémenter la solution (facultatif)

### Tâche 1 : intégrer Microsoft Defender pour point de terminaison à Defender for Cloud Apps

Pour contrôler les applications qui sont utilisées sur les appareils de l’entreprise, vous devez intégrer Defender pour point de terminaison à Defender for Cloud Apps.

1. Connectez-vous au portail Microsoft Defender **https://security.microsoft.com/** en tant qu’Allan Deyoung à l’aide de son compte d’**administrateur MOD**.
2. Dans le portail Microsoft Defender, développez **Repérage** et sélectionnez **Repérage avancé**. Attendez que la préparation des nouveaux espaces se termine.
3. Dans le portail Microsoft Defender, sur la page de navigation de gauche, sélectionnez **Paramètres**.
4. Sur la page **Paramètres**, sélectionnez **Points de terminaison**.
5. Sur la page **Points de terminaison**, sous **Général**, sélectionnez **Fonctions avancées**.
6. Activez **Microsoft Defender for Cloud Apps**.
7. Sélectionnez **Enregistrer les préférences** en bas.

Vous avez activé Microsoft Defender for Cloud Apps pour les points de terminaison. Avec cette configuration, tous les signaux provenant de Microsoft Defender pour point de terminaison sont transférés à Defender for Cloud Apps, ce qui vous permet de bloquer les applications non sécurisées. Toutes les applications étiquetées comme **non approuvées** seront désormais bloquées.

### Tâche 2 : examiner l’informatique fantôme de Contoso Ltd.

Dans cette tâche, vous allez analyser toutes les applications actuellement utilisées dans votre entreprise. Vous examinerez de plus près diverses applications et leur évaluation des risques respectifs ainsi que leur structure d’évaluation.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender **https://security.microsoft.com/**.
2. Dans le portail Microsoft Defender, dans la page de navigation de gauche, développez les **Applications cloud** et sélectionnez **Cloud Discovery**.
3. Sur la page **Cloud Discovery**, sélectionnez **Applications découvertes**.
4. Le panneau **Applications découvertes** affiche toutes les applications actuellement utilisées au sein de votre organisation. Explorez les applications et leurs scores de risque associés en les sélectionnant.

> [!NOTE] Defender for Cloud Apps évalue les risques selon les certifications réglementaires, les normes du secteur et les bonnes pratiques. Le score reflète le niveau d’adéquation de l’application à l’entreprise. Le score total de chaque application est calculé à partir de la moyenne des sous-scores pondérés dans différentes catégories de risques qui incluent des considérations relatives à la fiabilité.

Vous avez passé en revue plusieurs applications actuellement utilisées chez Contoso.

### Tâche 3 : bloquer les applications non sécurisées

Une fois que vous avez obtenu une vue d’ensemble de l’utilisation des applications dans votre environnement, votre première action de correction consiste à bloquer les applications non sécurisées.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender **https://security.microsoft.com/**.
2. Dans le portail Microsoft Defender, dans la page de navigation de gauche, développez les **Applications cloud** et sélectionnez **Cloud Discovery**.
3. Sur la page **Cloud Discovery**, sélectionnez **Applications découvertes**.
4. Définissez le filtre du **score de risque** entre 0 et 4.
5. Cliquez sur **Sélectionner en masse**, puis sur **Tout**.
6. Sélectionnez les trois points pour **plus d’actions**.
7. Sélectionnez **Marquer comme non approuvée**.
8. Cliquez sur **Enregistrer**.
   
Vous avez bloqué l’utilisation des applications vulnérables par les utilisateurs et les utilisatrices.

### Tâche 4 : bloquer automatiquement les applications non sécurisées

Pour bloquer automatiquement les applications non sécurisées, vous allez créer une stratégie de découverte d’applications personnalisée. Cette stratégie marque les applications non sécurisées comme **non approuvées**. Comme vous avez intégré Defender for Endpoint à Defender for Cloud Apps, ces applications sont automatiquement bloquées.

1. Vous devriez toujours vous trouver dans le portail Microsoft Defender **https://security.microsoft.com/**.
2. Dans le portail Microsoft Defender, dans la page de navigation de gauche, développez les **Applications cloud** et sélectionnez **Cloud Discovery**.
3. Sur la page **Applications découvertes**, sélectionnez **+ Nouvelle stratégie dans la recherche**.
4. Saisissez les informations suivantes :
    - **Nom de la stratégie** : marquer les applications non sécurisées comme non approuvées
    - **Gravité de la stratégie** : moyenne
    - **Description pour les utilisateurs et utilisatrices** : les applications avec un score de risque de 4 ou moins ne sont pas approuvées et sont automatiquement bloquées.
5. Sous **Applications correspondant à tous les éléments suivants**, ajoutez un filtre et définissez-le sur **Score de risque entre 0 et 4**.
6. Sous **Alertes**, sélectionnez **Créer une alerte pour chaque événement correspondant à la gravité de la stratégie** et définissez la valeur de **Limite d’alerte quotidienne par stratégie** sur 5.
7. Sous **Actions de gouvernance**, sélectionnez **Marquer l’application comme non approuvée**.
8. Sélectionnez **Créer**.

Vous avez créé une stratégie pour marquer des applications avec un score de risque de 4 ou moins comme non approuvées.