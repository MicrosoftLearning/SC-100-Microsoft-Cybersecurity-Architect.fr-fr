---
lab: 4
title: "Exercice\_3 - Protection contre la perte de données"
---

# Labo 4 - Exercice 3 - Protection contre la perte de données

Contoso Ltd. intègre actuellement Tailwind Traders à leurs projets. Bien que la fusion soit toujours en cours, les deux entreprises travaillent dans des locataires distincts. Les employés de Tailwind Traders sont considérés comme des utilisateurs et utilisatrices externes et se connectent en tant qu’invités au locataire de Contoso pour faciliter le partage de sites et de fichiers SharePoint. Dans certains projets, certains employés de Tailwind Traders reçoivent des clients Windows 11 gérés par Contoso Ltd. pour garantir un accès total aux ressources internes tout en conservant la surveillance de la sécurité. L’accès aux applications de bureau M365 est bloqué pour les appareils non gérés, et ces utilisateurs et utilisatrices peuvent uniquement accéder à l’environnement via des applications Web. Les appareils gérés sont sécurisés par le biais de différentes stratégies dans le Gestionnaire de points de terminaison. Contoso Ltd. a implémenté la Protection des données Microsoft Purview pour chiffrer des documents sensibles en fonction du type d’informations qu’ils contiennent. 

En tant qu’architecte en cybersécurité, vous avez récemment examiné diverses activités dans le journal d’activité Defender for Cloud Apps et découvert que certains documents marqués comme confidentiels sont copiés sur des lecteurs USB externes. Vous avez également découvert que les utilisateurs et utilisatrices sont libres de stocker les données d’entreprise auxquelles ils ont accès sur leurs appareils personnels non gérés. Cela pose un sérieux problème qui doit être résolu. En guise de solution, vous allez concevoir une stratégie de sécurité pour restreindre le stockage des données d’entreprise sur des appareils personnels non gérés. Cela permet de réduire le risque d’exposition des données sensibles.

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour répondre aux risques auxquels Contoso Ltd. est confronté.

### Approche de conception

La première étape consiste à analyser les exigences en fonction du problème décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Empêcher le transfert de données vers des lecteurs USB
- Limiter l’accès aux données sensibles à partir d’appareils non gérés
- Bloquer les téléchargements de données sensibles sur des appareils non gérés

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Purview et Microsoft Defender offrent différentes solutions pour gérer le flux de données, englobant la Protection des données Microsoft Purview, la protection contre la perte de données, l’accès conditionnel et les stratégies de rétention. Examinez les contrôles déjà en place. Accédez à différents portails pour examiner les configurations et stratégies actuelles et déterminer si des ajustements sont nécessaires ou si de nouveaux paramètres/stratégies devraient être implementés.

La troisième phase implique l’élaboration du concept de solution. L’examen des stratégies actuelles permet de conclure qu’aucune d’entre elles ne répond aux exigences définies. Par conséquent, un nouvel ensemble de stratégies doit être créé.

### Solution proposée

Concevez une stratégie de sécurité pour restreindre le stockage des données d’entreprise sur des appareils personnels non gérés. Cela permet de réduire le risque d’exposition des données sensibles. La stratégie doit décrire les types de données considérés comme sensibles et les appareils sur lesquels elles peuvent être stockées. En outre, la stratégie doit fournir des instructions sur le transfert sécurisé de données vers des appareils externes. Les employés doivent signer un accord reconnaissant qu’ils ont compris la stratégie et qu’ils s’engagent à la respecter. La stratégie doit être communiquée à tous les employés et appliquée par le biais d’audits réguliers et d’actions disciplinaires en cas de non-respect. Des sessions de formation régulières doivent également avoir lieu pour s’assurer que les employés sont conscients des risques associés au stockage des données de l’entreprise sur des appareils personnels et de l’importance de respecter la stratégie. Enfin, la stratégie doit être examinée et mise à jour régulièrement pour s’assurer qu’elle reste efficace et pertinente. 

|Exigence|Solution|Plan d’action|
|----|----|----|
|Bloquer le transfert de données vers des lecteurs USB|Protection contre la perte de données de point de terminaison|Bloquer la copie de toutes les données avec une étiquette sensible vers un lecteur USB|
|Restreindre l’accès aux données sensibles à partir d’appareils non gérés|Defender for Cloud Apps|Bloquer les actions copier/couper/coller des données pour les appareils non gérés|
|Bloquer les téléchargements de données sensibles sur des appareils non gérés|Defender for Cloud Apps|Bloquer le téléchargement de données à partir d’appareils non gérés|

## Partie 2 : implémenter la solution (facultatif)

### Tâch 1 : déployer une stratégie de protection contre la perte de données

La première étape de la conception de la solution consiste à créer une règle de protection contre la perte de données pour les points de terminaison. Vous allez déployer une règle DLP pour bloquer la copie de données sur des lecteurs USB. 

1. Connectez-vous au portail de conformité Microsoft Purview **https://compliance.microsoft.com** en tant qu’Allan Deyoung à l’aide de son compte d’**administrateur MOD**.
1. Si un message vous invite à revenir au portail de conformité Microsoft Purview classique, sélectionnez **Basculer**.
1. Dans le portail Microsoft Purview, dans le volet de navigation, développez **Protection contre la perte de données**, puis sélectionnez **Stratégies**.
1. Dans la page **Stratégies**, sélectionnez **+ Créer une stratégie**.
1. Sur la page **Démarrer avec un modèle ou créer une stratégie personnalisée**, sélectionnez **Personnaliser**, puis **Stratégie personnalisée** et enfin **Suivant**.
1. Sur la page **Nom de votre stratégie DLP**, entrez un nom et une description, puis sélectionnez **Suivant**.
1. Sur la page **Affecter des unités d’administration**, sélectionnez **Suivant**.
1. Sur la page **Choisir où appliquer la stratégie**, sélectionnez uniquement **Appareils**, puis **Suivant**.
1. Sur la page **Définir les paramètres de stratégie**, sélectionnez **Suivant**.
1. Sur la page **Personnaliser les règles DLP avancées**, sélectionnez **+ Créer une règle**.
1. Entrez un nom et une description pour la règle. 
1. Sous **Conditions**, sélectionnez **+ Ajouter une condition**, puis **Le contenu inclut**.
1. Spécifiez les conditions suivantes :

    - **Le contenu inclut** : 
      - Sélectionnez **Ajouter**, puis sélectionnez **Étiquettes de confidentialité**, puis sélectionnez les étiquettes **Personnes approuvées**, **Projet - Falcon**, **Confidentiel**, **Hautement confidentiel**, **Confidentiel - Finance**. Cliquez sur **Ajouter**.
13. Sous **Actions**, sélectionnez **+ Ajouter une action**, puis sélectionnez **Auditer ou restreindre les activités sur les appareils**.
14. Spécifiez les actions suivantes :
   -    Sous **Activités de fichier pour toutes les applications**, sélectionnez **Appliquer des restrictions à une activité spécifique**.
      - Vérifiez que **Copier sur un périphérique USB amovible** est sélectionné et sélectionnez l’option **Bloquer** dans le menu déroulant de ce paramètre.
      - Laissez les autres paramètres inchangés.
15. Cliquez sur **Enregistrer**.
16. Cliquez sur **Suivant**.
17. Sur la page **Mode de stratégie**, sélectionnez **Activer immédiatement la stratégie**. Cliquez sur **Suivant**.
18.  Dans la page **Vérifier et terminer**, sélectionnez **Envoyer**.

Vous avez implémenté une stratégie de protection contre la perte de données qui bloque toute copie de données sur des lecteurs USB.

### Tâche 2 : intégrer des applications au contrôle d’application par accès conditionnel

Une partie de la solution consiste à créer des stratégies de session dans Defender for Cloud Apps. Les stratégies de session offrent un aperçu complet des applications cloud par le biais d’une surveillance en temps réel des sessions. Ces stratégies permettent des actions personnalisées en fonction de la stratégie spécifiée pour chaque session utilisateur. Pour créer une stratégie de session, vous devez déployer le contrôle d’application par accès conditionnel sur vos applications. Le contrôle d’application par accès conditionnel ajoute des capacités de surveillance et de contrôle en temps réel à vos applications. Créer une stratégie de session sans intégrer une application au contrôle d’application par accès conditionnel ne fonctionne pas. La première étape consiste à intégrer des applications que vous souhaitez protéger au contrôle d’application par accès conditionnel. 

Il existe deux façons d’intégrer des applications au contrôle d’application par accès conditionnel :

- Ajouter une application manuellement dans le portail Microsoft Defender (Paramètres > Applications cloud > Applications connectées > Applications du contrôle d’applications par accès conditionnel)
- Configurer une stratégie d’accès conditionnel pour protéger les applications avec Defender for Cloud Apps

Une stratégie d’accès conditionnel transfère toutes les applications spécifiées dans la stratégie à « Contrôle d’application par accès conditionnel Defender for Cloud Apps ». La prochaine fois qu’un utilisateur ou une utilisatrice se connecte à l’une des applications spécifiées, elle sera automatiquement ajoutée au contrôle d’application par accès conditionnel. Vous pouvez afficher ces applications dans le portail Microsoft Defender. 
 
>**Conseil :** avant de commencer cette tâche, vous devez vérifier les applications existantes du contrôle d’application par accès conditionnel. Vous remarquerez qu’aucune application n’a été intégrée pour le moment. À ce stade, essayez de créer une stratégie de session dans Defender for Cloud Apps et vérifiez les messages d’erreur.

Dans cette tâche, vous allez déployer le contrôle d’application par accès conditionnel sur vos applications en créant une stratégie d’accès conditionnel dans Microsoft Entra. 

1. Connectez-vous au portail Microsoft Entra **https://entra.microsoft.com** en tant qu’Allan Deyoung à l’aide de son compte d’**administrateur MOD**.
2. Dans le portail Microsoft Entra, développez **Protection** et sélectionnez **Accès conditionnel**.
3. Sur la page **Accès conditionnel | Vue d’ensemble**, sélectionnez **Stratégies**, puis cliquez sur **+ Nouvelle stratégie**.
4. Permet d’entrer un nom pour la stratégie.
5. Sous **Affectations,** sélectionnez **Utilisateurs** et incluez **Tous les utilisateurs**.
6. Sous **Affectations**, sélectionnez **Ressources cibles** et incluez **Toutes les applications cloud**.
7. Sous **Contrôles d’accès**, sélectionnez **Session**.
8. Dans le volet **Session**, sélectionnez **Utiliser le contrôle d’application par accès conditionnel** et **Utiliser une stratégie personnalisée...**, puis fermez le volet **Session** avec le bouton **Sélectionner**.
9. Sous **Activer une stratégie**, sélectionnez **Activé**.
10. Si vous recevez un avertissement vous invitant à exclure l’utilisateur actuel de la stratégie, sélectionnez **Je comprends que mon compte sera affecté par cette stratégie. Continuer quand même.**.
11. En option, spécifiez les conditions et les contrôles d’octroi.
12. Sélectionnez **Créer**.

Connectez-vous maintenant à une application web Microsoft, comme [Outlook](https://outlook.office365.com). L’application à laquelle vous vous connectez sera automatiquement intégrée au contrôle d’application par accès conditionnel. Connectez-vous au portail Microsoft Defender et affichez les applications sous contrôle d’application par accès conditionnel.

Vous avez créé une stratégie d’accès conditionnel pour transférer toutes les applications à Defender for Cloud Apps et les applications intégrées au contrôle d’application par accès conditionnel.

### Tâche 3 : créer des stratégies de session dans Defender for Cloud Apps

Vous allez créer deux stratégies de session dans Defender for Cloud Apps afin de bloquer les téléchargements de données et de restreindre les autorisations pour les appareils non gérés.

1. Connectez-vous au portail Microsoft Defender **https://security.microsoft.com** en tant qu’Allan Deyoung à l’aide de son compte d’**administrateur MOD**.
1. Dans le portail Sécurité Microsoft, sélectionnez **Applications cloud** > **Stratégies** > **Gestion des stratégies**.
1. Sur la page **Stratégies**, sélectionnez **+ Créer une stratégie** > **Stratégie de session**.
1. Sur la page **Créer une stratégie de session**, sélectionnez le modèle de stratégie **Bloquer le téléchargement en fonction de l’inspection du contenu en temps réel**.
1. Entrez un nom de stratégie.
1. Sélectionnez la gravité de la stratégie et une catégorie.
1. Saisissez une description.
1. Sous **Type de contrôle de session**, sélectionnez **Contrôler le téléchargement de fichiers (avec inspection)**.
1. Sous **Source de l’activité** dans la section **Activités remplissant toutes les conditions suivantes**, sélectionnez les filtres suivants :

    - **Balise d’appareil** : sélectionnez **Ne correspond pas**, puis **Conforme à Intune**.

10. Dans la section **Fichiers remplissant toutes les conditions suivantes**, sélectionnez les filtres suivants :

    - **Étiquette de confidentialité** : sélectionnez **Correspond** et sélectionnez les étiquettes **Confidentiel**, **Hautement confidentiel** et **Confidentiel - Finance**.

11. Sous **Méthode d’inspection**, sélectionnez **Service de classification des données**, puis **Tout**, puis **Type d’informations sensibles...** et sélectionnez le type d’informations sensibles auquel vous souhaitez appliquer cette stratégie.
12. Sous **Actions**, sélectionnez **Bloquer**.
13. Sélectionnez **Créer** pour créer la stratégie.
14. Créez une deuxième stratégie comme décrite ci-dessus, puis sélectionnez le modèle de stratégie **Bloquer les actions couper/copier/coller en fonction de l’inspection du contenu en temps réel**.
15. Sous **Source de l’activité** dans **Activités remplissant toutes les conditions suivantes**, sélectionnez les filtres suivants : 

    - **Type d’activité** : sélectionnez **Correspond**, puis **Couper/copier l’élément, coller l’élément**.
    - **Balise d’appareil** : sélectionnez **Ne correspond pas**, puis **Conforme à Intune**

16. Désactivez **Utiliser l’inspection du contenu** et sélectionnez **Créer** pour créer la stratégie.

Vous avez créé deux stratégies de session dans Defender for Cloud Apps.
