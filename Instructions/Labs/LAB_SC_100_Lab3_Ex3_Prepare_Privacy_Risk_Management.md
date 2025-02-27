---
lab: 3
title: "Exercice\_3 - Préparer la gestion des risques liés à la confidentialité"
---


# Labo 3 - Exercice 3 - Préparer la gestion des risques liés à la confidentialité

En tant qu’expert architecte en cybersécurité pour Contoso, vous devez améliorer l’état de la conformité de l’entreprise dans le cadre de son expansion européenne. Vous allez vous concentrer sur l’amélioration du score Gestion des risques de confidentialité Priva. Pour ce faire, vous allez utiliser le Gestionnaire de conformité pour identifier les actions d’amélioration et déléguer leur implémentation. Cela permettra d’améliorer le score de conformité de la gestion des risques de confidentialité. Vous allez également ajouter une nouvelle stratégie pour les régions des États-Unis et de l’UE. 

## Partie 1 : concevoir une solution (obligatoire)

Dans cette tâche, vous allez concevoir un concept pour remplir les exigences de Contoso Ltd.

### Approche de conception

L’étape initiale consiste à analyser les exigences en fonction du scénario décrit, à comprendre les objectifs et à définir les exigences.

En fonction du cas d’utilisation, les exigences suivantes peuvent s’avérer pertinentes :

- Les équipes d’administration et les autres personnes ayant accès aux rapports ne doivent pas voir les noms des utilisateurs et utilisatrices
- Les risques de confidentialité doivent être gérés par une équipe désignée
- Les directives doivent exister pour les risques de confidentialité

Dans la deuxième étape, examinez l’environnement existant de Contoso Ltd.. Microsoft Priva offre des solutions pour gérer les risques de confidentialité. Examinez les contrôles et les stratégies actuels. Utilisez le portail de conformité Microsoft Purview pour passer en revue les configurations actuelles et déterminer les ajustements qui doivent être implémentés pour répondre aux exigences de la région vers laquelle ils s’étendent.

La troisième phase consiste à élaborer le concept de la solution. L’examen permet de conclure qu’il est évident que la création de stratégies pour surveiller les risques potentiels est la meilleure façon de répondre aux exigences.  

### Solution proposée

|Exigence|Solution|Plan d’action|
|----|----|----|
|Les équipes d’administration et les autres personnes ayant accès aux rapports ne doivent pas voir les noms des utilisateurs et utilisatrices|Action d’amélioration de la conformité|Affecter et implémenter l’action d’amélioration **Rendre les noms des utilisateurs et utilisatrices anonymes pour les personnes avec certains rôles**|
|Les risques de confidentialité doivent être gérés par une équipe désignée|Rôles Microsoft Purview|Créer un groupe de rôles avec des autorisations pour gérer les risques de confidentialité et affecter les employés désignés|
|Les directives doivent exister pour les risques de confidentialité|Stratégies de gestion des risques de confidentialité|Créer une stratégie de gestion des risques de confidentialité pour alerter l’équipe responsable des risques potentiels|

## Partie 2 : implémenter la solution (facultatif)

## Tâche 1 : examiner les actions d’amélioration possibles du Gestionnaire de conformité pour la gestion des risques de confidentialité et leur attribuer des propriétaires

Dans cette tâche, vous obtenez une vue d’ensemble des actions d’amélioration possibles de la gestion des risques de confidentialité et les déléguer.

1. **Connectez-vous** au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
2. Dans le volet de gauche, sélectionnez **Vue d’ensemble de la gestion des risques de confidentialité**.
3. Faites défiler vers le bas jusqu’à la carte **Rester conforme aux réglementations et améliorer l’état de la confidentialité**.
4. Sélectionnez le bouton **Afficher les actions d’amélioration**.
5. Examinez les actions d’amélioration possibles. Réfléchissez aux actions d’amélioration que vous pouvez configurer au préalable et que vous pouvez déléguer à l’équipe de sécurité.
6. Sélectionnez l’action d’amélioration **Activer les administrateurs des opérations de confidentialité pour créer et prendre en charge le traitement des demandes des personnes concernées**.
7. Lisez les détails de l’amélioration.
8. Affectez **Megan Bowen** en tant que propriétaire de l’action d’amélioration à l’aide du menu déroulant.
9. En haut de la page, sélectionnez **Modifier les détails**.
10. Définissez le **statut de l’implémentation** sur **Implémenté**. Vous avez affecté **Megan Bowen** à deux groupes de rôles, Administrateur des demandes des personnes concernes et Administrateur de la gestion des risques de confidentialitée, dans l’exercice précédent.
11. Sélectionnez **Enregistrer et fermer** en bas de la page.

Vous avez correctement affecté une action d’amélioration à un employé de sécurité.

## Tâche 2 : Affecter et implémenter l’action d’amélioration **Anonymiser les noms d’utilisateur aux utilisateurs dans certains rôles**

Vous devez vous assurer que les utilisateurs sont anonymisés dans tous les composants Priva pour l’action d’amélioration.

*Passez à l’étape 5 si vous êtes toujours sur la **vue d’ensemble des actions d’amélioration.***
1. **Connectez-vous** au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
1. Sélectionnez **Gestionnaire de conformité** > **Actions d’amélioration**.
1. Sélectionnez l’action d’amélioration **Anonymiser les noms d’utilisateur aux utilisateurs dans certains rôles**.
1. À l’aide du menu déroulant, identifiez-vous comme **Administrateur MOD** et propriétaire de cette action d’amélioration.
1. Sous **Détails**, sélectionnez le lien **Lancer maintenant** à la fin de la description **Comment implémenter**.
1. Vérifiez que le paramètre **Afficher les versions anonymisées des noms des utilisateurs** est sélectionné, sinon, sélectionnez-le, puis choisissez **Enregistrer**.
1. Fermez l’onglet du navigateur.
1. Sélectionnez **Modifier les détails** en haut de l’action d’amélioration **Afficher les versions anonymisées des noms des utilisateurs et utilisatrices**.
1. Définissez le **statut de l’implémentation** sur **Implémenté** et sélectionnez **Enregistrer**.
1. Sélectionnez **Enregistrer et fermer** en bas de la page.

Vous avez affecté et implémenté une action d’amélioration.

## Tâche 3 : créer une stratégie de gestion des risques de confidentialité

Cette dernière tâche consiste à créer la politique de gestion des risques de confidentialité personnalisée pour les régions de l’UE et des États-Unis.

1. Accédez au **portail de conformité Microsoft Purview****https://compliance.microsoft.com/**.
2. Dans le volet de gauche, sélectionnez **Gestion des risques de confidentialité** > **Stratégies**.
3. Sélectionnez **Créer une stratégie** en haut à droite.
4. Sélectionnez **Créer** dans la carte **Personnaliser**.
5. Sélectionnez le modèle de stratégie **Minimisation des données**.
6. Entrez le nom de la stratégie :**Minimisation des données pour les États-Unis et l’UE**.
7. Entrez la description :**cette stratégie vise à minimiser les données relatives aux risques de confidentialité enregistrées en fonction des réglementations américaines et européennes.**
8. Cliquez sur **Suivant**.
9. Sélectionnez **Ajouter des groupes de classification**.
10. Sélectionnez :
    - RGPD - Amélioré
    - U.S. Gramm-Leach-Bliley Act (GLBA) - Amélioré
    - Loi américaine sur l’assurance maladie (HIPAA) - Amélioré
    - U.S. Patriot Act - Amélioré
    - Données d’information personnelle (PII) américaines - Amélioré
    - Lois sur les notifications des violations de données d’état des États-Unis - Amélioré
11. Sélectionnez **Ajouter** et **Enregistrer**.
12. Sélectionnez tous les utilisateurs et les groupes, puis **Suivant**.
13. Sélectionnez tous les emplacements, puis **Suivant**.
14. Définissez le paramètre **L’élément n’a pas été modifié au cours des derniers (jours)** sur 120.
15. Pour **Choisir la fréquence des notifications**, sélectionnez **Mensuellement, tout les 1**.
16. Pour **Lien vers la formation sur la confidentialité**, entrez : https://learn.microsoft.com/en-us/privacy/
17. Cliquez sur **Suivant**.
18. Définissez **Créer des alertes** sur **Activé**.
19. Définissez **Volume élevé de données personnelles** sur 20 instances.
20. Cliquez sur **Suivant**.
21. Cliquez sur **Suivant**.
22. Vérifier les paramètres, puis sélectionnez **Soumettre**.

Vous avez créé une politique de gestion des risques de confidentialité pour les lois américaines et européennes sur la protection des données.

Vous avez terminé la configuration et la délégation des actions d’amélioration, des stratégies de gestion des risques de confidentialité et des autorisations utilisateur. Vous pouvez passer à l’exercice suivant.
