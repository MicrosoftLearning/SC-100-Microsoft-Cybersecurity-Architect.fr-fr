---
casestudy:
  title: "Étude de cas\_: stratégie face aux ransomwares"
  module: 'Module 13: Recommend a ransomware strategy by using Microsoft Security Best Practices'
---
Cet exercice d’étude de cas permet d’acquérir une expérience dans l’exécution de certaines tâches d’étude conceptuelle liées aux sujets appris dans ce module.

## Étude de cas : recommander une stratégie face aux ransomwares basée les bonnes pratiques de sécurité Microsoft
 
CONTOSO est une société de services de santé dont les bureaux principaux sont établis à Chicago et Londres, au Royaume-Uni.  
La société fournit des services de santé à ses clients dans ses installations situées à Chicago et dans la zone métropolitaine de Londres, au Royaume-Uni.  Les installations de Contoso comptent de nombreux hôpitaux disposant de médecins, d’infirmières et d’autres professionnels de la santé. Contoso a lancé la migration à l’échelle de l’entreprise de tous les services critiques vers le cloud. Cette migration inclut les serveurs locaux, les machines virtuelles et les appliances de gestion et de surveillance qui y sont associées.

Contoso a lancé sa migration vers le cloud, à l’exception de certaines données et applications qui doivent être hébergées localement en raison des exigences réglementaires et de conformité. Contoso dispose d’un locataire Azure Active Directory (Azure AD). Cet Azure AD est synchronisé avec Active Directory Domain Services (AD DS), qui est géré sur des contrôleurs de domaine locaux. À mesure que la migration progresse, des abonnements Azure supplémentaires seront créés selon les besoins de chaque service, y compris les applications SaaS. Pour faciliter leur travail quotidien, la plupart des employés ont accès aux applications Microsoft 365.  
 
Il y a eu plusieurs cas récents très médiatisés d’attaque par ransomware impliquant les concurrents de Contoso sur le marché des services de santé. Le PDG et le CISO sont préoccupés par le fait que Contoso n’a pas encore mis en place de plan pour atténuer le risque d’une attaque par ransomware. Le CISO a personnellement demandé que vous élaboriez un plan de réaction et d’atténuation du risque d’attaque par ransomware, que vous présenterez aux dirigeants de l’entreprise dans deux semaines. Certains des membres du personnel informatique les plus haut gradés ont clamé que la menace de ransomware est exagérée et que l’entreprise a seulement besoin de bonnes sauvegardes et d’une sécurité du périmètre rigoureuse.
 
### Configuration requise

* Le plan de réponse et d’atténuation du risque d’attaque par ransomware doit inclure non seulement l’infrastructure locale critique et les services cloud, mais également les données de l’entreprise stockées sur les ordinateurs portables de l’entreprise et les appareils mobiles utilisés par les employés sur le terrain.
* Le PDG et le CISO ont adopté une approche dure stipulant qu’ils ne paieront jamais les pirates informatiques à l’origine d’un ransomware ou ne négocieront jamais avec eux. Ils ont déclaré qu’en cas d’attaque par ransomware, leur objectif est de rétablir les systèmes critiques dans les 12 heures, et de restaurer les fonctionnalités complètes dans les 48 heures.
* Les stratégies de gestion des données doivent respecter les exigences de confidentialité, notamment la loi HIPAA aux États-Unis et toutes les normes connexes au Royaume-Uni.
* Votre plan doit également expliquer pourquoi une bonne sauvegarde ne suffit pas à atténuer la menace d’une attaque par ransomware.

### Premières questions

* Quels services et employés faut-il impliquer dans l’élaboration du plan d’atténuation du risque d’attaque par ransomware ? 
* Sur quels services et éléments d’infrastructure le plan doit-il porter ? 
* Quels sont les délais réalistes d’élaboration d’un plan rigoureux de réponse aux attaques par ransomware ?
* Quels sont les principaux indicateurs du succès de l’implémentation de votre plan de protection contre les ransomwares ?

### Tâches de conception

* Répertorier les services Azure et M365 sera essentiel à la sauvegarde et à la sécurisation de vos données. Expliquer pourquoi chaque service fait partie intégrante de la réponse à une attaque par ransomware et préciser les compromis que chacun d’eux implique.
* Prendre note des exigences particulières de votre entreprise auxquelles les solutions Azure et M365 existantes ne répondent pas.
* Répertorier les services et les éléments d’infrastructure qui doivent être traités par le plan.
* Estimer les délais réalistes d’élaboration d’un plan rigoureux de réponse aux attaques par ransomware, puis exécuter ce plan. 