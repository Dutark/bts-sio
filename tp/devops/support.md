# Complément du cours Dev Ops

Ce document est un complément du cours. Il vous permettra de revenir sur les différentes notions avec différents exemples.

::: details Table des matières
[[toc]]
:::

## Introduction

Le terme « Full Stack » est un gros mot, il se cache derrière plein de définitions différentes. Nous allons voir un aspect de celui-ci dans ce document et dans nos échanges.

Nous allons découvrir comment vous allez pouvoir « Développer, Tester, Déployer » sans vous prendre la tête avec différentes technologies qui sont maintenant la base de tout bon développeur (Docker, l'intégration Continue, la JamaStack, les Function As A Service − FaaS −). L'idée étant qu'à la fin de ce document vous soyez capable de construire, maintenir, mais également comprendre la révolution « Cloud » autour du métier du développeur.

Nous allons donc voir comment le développeur seul sera capable de mettre en place une infrastructure d'exécution de son application ; cette infrastructure sera complètement automatisée pour « se recréer » / « se mettre à jour » en fonction des actions (commit) que vous ferez dans votre code source. J'ai utilisé le terme « commit », car oui, cette automatisation est possible en grande partie grâce à notre système de version de sources (par exemple, GIT).

Je vous propose de commencer notre pèlerinage par la découverte de Docker.

## Docker

![Docker](./res/0_8joZxa9NhRqDjHva.png)

### Introduction

Docker c'est « une petite révolution » ! Docker est une plateforme datant de 2013 permettant aux développeurs de déployer, mais également d'exécuter des applications avec **des conteneurs**. Docker permet de packager une application (ainsi que ses dépendances) dans un process isolé nommé conteneur. Ce conteneur peut ensuite être exécuté sur n'importe quelle machine (ARM, X86…), mais également sur n'importe quel système d'exploitation (Linux, Windows, macOS).

Docker est une technologie française, mais celle-ci est utilisée mondialement ; elle est devenue un standard en très peu de temps ce qui en fait un incontournable à connaitre pour vous développeur. Et vous allez le voir, celle-ci va vous faire gagner un temps fou !

### Containers ou Machines virtuelles ?

### Créer des machines simplement

### Le DockerFile

### Le Docker Compose

### Les alternatives

### Une stack complète sur un Raspberry Pi

Nous l'avons vu dans les différents exemples précédents, Docker est un vrai petit bijou pour la conception du « stack » applicative. C'est en partant de cette constatation que j'ai décidé de créer moi-même une « Stack » permettant de créer un serveur d'évaluation / de développement personnel basé sur du matériel « pas cher » à savoir un Raspberry Pi.

Une solution qui dans mon cas ressemble à :

| ![Version 1](../rpi/res/version1.jpg) | ![Version 2](../rpi/res/version2.jpg) |
| ------------------------------------- | ------------------------------------- |


[Lire la suite](../rpi/web-stack.md)

## CI / CD

### Introduction

### CI (Intégration Continue)

### CD (Déploiement Continu / Livraison Continue)

#### Les tests

#### Les artifacts

## Gitlab CI

### Introduction

### Gitlab Pages

### Tester en continu

### Compilation d'application

## Netlify

### La JamStack ?

La jamstack c'est une nouvelle façon de voir la conception de site Internet, cette nouvelle façon de faire va nous permettre de réduire les couts d'hébergements / et bénéficier de l'avantage du Cloud (CI/CD, compression des assets, FAAS…)

Plein de mots qui font peur, mais ne vous inquiétez pas… C'est beaucoup plus simple qu'il n'y parait. Ici pas de PHP pour générer vos pages nous allons tout concevoir en HTML / JavaScript (VanillaJS, React, Vue, …) / CSS

![JamStack](./res/jamstack-horizontal.svg)

### Déployer un site automatiquement

Ici pas de blabla, Netlify est une solution pensée pour être simple ; je vous propose donc de directement mettre en application via [le TP suivant](../ci/jamstack/netlify.md)

## OpenFaas

### Introduction

### Déployer sur OpenFaas