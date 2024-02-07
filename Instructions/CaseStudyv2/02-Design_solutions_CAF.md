---
casestudy:
  title: "Étude de cas\_: concevoir des solutions qui s’alignent sur le CAF (Cloud\_Adoption\_Framework)"
  module: 'Module 02: Design solutions that align with CAF and WAF'
---
Cet exercice d’étude de cas permet d’acquérir une expérience dans l’exécution de certaines tâches d’étude conceptuelle liées aux sujets appris dans ce module.

## Étude de cas : concevoir des solutions qui s’alignent sur le CAF (Cloud Adoption Framework)

- Contoso Banking est une filiale de Contoso Group, qui est en train de devenir une entité commerciale indépendante. Contoso Banking sera une entreprise distincte dotée de sa propre infrastructure et de sa propre organisation informatique. 
- L’infrastructure de Contoso Banking sera entièrement basée sur le cloud Microsoft Azure. Pour construire une plateforme cloud sécurisée dès la création de l’entreprise, vous devez concevoir une zone d’atterrissage Azure sécurisée.
- En vertu des conditions de l’accord, la transition doit prendre au maximum 6 mois
- Contoso Banking prévoit de créer la solution FinTech de nouvelle génération à l’aide de solutions natives cloud. La version MVP 1 doit être terminée dans 6 semaines.

### Configuration requise

Contoso Group n’utilise aucun service cloud, l’infrastructure est entièrement hébergée dans son propre centre de données. L’environnement qui fera partie de Contoso Banking inclut :

- Environnement 1 : systèmes bancaires de bas : 20 applications. La sécurité est un aspect essentiel.
- Environnement 2 : application de nouvelle génération / Fintech, basée sur Azure Kubernetes Service et Azure Data Lake. 100 versions par mois

#### Changements planifiés

Environnement 1 : Contoso Banking prévoit de déplacer toute l’infrastructure bancaire principale vers le cloud. L’approche doit inclure les éléments suivants :

- Déployer une zone d’atterrissage là où les applications principales sont hébergées.
- Les utilisateurs doivent accéder aux applications principales à partir de stations de travail cloud sécurisées. Les utilisateurs doivent posséder une expérience utilisateur cohérente pour accéder aux applications.
- La solution doit garantir le respect des bonnes pratiques en matière de gestion des identités et des accès, de gouvernance, de sécurité, de réseau et de journalisation.

L’environnement 2 (application Fintech) doit répondre aux exigences suivantes :

- 100 versions/mois
- Être en permanence prêt pour l’audit
- Se conformer à PCI-DSS

### Tâches de conception

- Quels sont les composants nécessaires à déployer dans la zone d’atterrissage ?
- Comment le choix des charges de travail affectera-t-il le délai et la complexité de l’implémentation ?
- Comment implémenteriez-vous l’accès sécurisé aux applications principales ?
- Quelle zone d’atterrissage Azure devez-vous recommander à Contoso Banking d’implémenter pour l'environnement 1 ?
- Quelle zone d’atterrissage Azure devez-vous recommander à Contoso Banking d’implémenter pour l'environnement 2 ?
