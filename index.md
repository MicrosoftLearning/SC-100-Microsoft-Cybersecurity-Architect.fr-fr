---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
---

# Répertoire de contenu

Les liens hypertexte vers chaque étude de cas sont répertoriés ci-dessous.


## Études de cas réorganisées pour l’actualisation du contenu de mai 2023

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudyv2/'" %}
| Module | Étude de cas |
| --- | --- | 
{% pour l’activité dans l’étude de cas %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}


## Ancienne organisation d’étude de cas

{% assign casestudy= site.pages | where_exp:"page", "page.url contains '/Instructions/CaseStudy/'" %}
| Module | Étude de cas |
| --- | --- | 
{% pour l’activité dans l’étude de cas %}| {{ activity.casestudy.module }} | [{{ activity.casestudy.title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}