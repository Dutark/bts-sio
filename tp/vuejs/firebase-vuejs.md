# Firebase + Vuejs

Dans ce TP nous allons découvrir Firebase RealtimeDB (base de données temps réel). Nous allons coupler cette base de données temps réel à la puissance de VueJS pour obtenir en un rien de temps une WebApplication surpuissante.

## Introduction

Dans ce TP nous allons mettre en place une carte temps réel qui utilise comme base de données la Realtime Database de firebase.

TODO IMAGE

## La mise en place

Nous allons utiliser VueCLI pour initialiser le projet, première étape l'installation

## Installer NodeJS + VueCLI

Avant de commencer nous allons avoir besoin de plusieurs outils :

- NodeJS
- Vue-cli

## NodeJS

La première étape va être l’installation de NodeJS, la démarche est différente en fonction de votre environnement, mais pour résumer [sous Windows c’est ici](https://nodejs.org/en/download/) prendre la version CURRENT, sous OSX le plus simple c’est via Brew `brew install nodejs`, et sous Linux c’est via le gestionnaire de paquet `apt install nodejs`

Une fois installé, vous êtes prêt, votre PC est prêt à accueillir l’outil VueCLI

## Vue-cli

Vue-cli est un outil qui simplifie la création d’un nouveau projet Vue-JS à partir de template fourni par la communauté.

Dans un terminal lancer la commande suivante dans le `Node.js Command Prompt` :

```shell
npm install -g @vue/cli
```

Maintenant que vue-cli est installé, vous avez à votre disposition sur votre ordinateur une nouvelle commande, la commande `vue`

Pour créer un nouveau projet, c’est simple il suffit de lancer la commande suivante dans le `Node.js Command Prompt`

## Initialiser le projet

La création d'un nouveau projet est très simple. Il suffit de rentrer la commande suivante :

```js
vue-cli create firebase-vuejs
```

Choisir l'option « Default ».

⚠️ Le projet est créé dans le dossier courant. Veuillez à saisir la commande dans un dossier vide.

🤓 git est déjà initialisé, vous pouvez en profiter pour pusher votre code sur Github.

### Questions

- Pourquoi git est déjà analysé ?
- Allez jeter un coup d'oeil au fichier `.gitignore`

## Tester

Le projet initialisé par `vue-cli` est imédiatement fonctionnel. Tester le en saisissant :

```js
npm run serve
```

![VueJS init](./ressources/vuejs-init.png)

## Les dépendances

Maintenant que notre projet est « initialisé », nous allons avoir besoin de quelques dépendances NPM pour faire fonctionner notre projet. Notre projet va utiliser les technologies suivantes :

- firebase
- leaflet

Firebase comme vous le savez va nous servir de système de base de données. [Leaflet](http://leafletjs.com/) quand à lui est une librairie qui vas nous permettre d'afficher très rapidement une carte sur notre site internet.

### Ajouter les dépendances

Les deux outils / librairie que nous allons utiliser sont disponible via NPM, nous allons donc les installer / ajouter au projet via les commandes suivantes :

```bash
npm install firebase vue2-leaflet --save
```

### Configuration de la dépendance carte

Certains plugins nécéssitent de la configuration supplémentaire, ça sera le cas pour Vue2-Leaflet (et Firebase), comme vous je ne connais pas la configuration de l'ensemble des dépnedances existante. Première étape :

- [Lire la documentation sur le site de Vue2-Leaflet](https://korigan.github.io/Vue2Leaflet/#/quickstart.md)

Maintenant que nous avons vu comment s'intègre le projet, refléchissons comment intégrer ça dans notre projet :

- À l'arrache dans le fichier `main.js` ? ✋ => NON
- Dans un dossier `plugins` => 👍 Oui

À votre avis pourquoi ?

### Création de la partie plugin

Créer le fichier `src/plugins/vue2-leaflet.js` y mettre dedans :

```js
import { L } from "vue2-leaflet";
import "leaflet/dist/leaflet.css";

// this part resolve an issue where the markers would not appear
delete L.Icon.Default.prototype._getIconUrl;

L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png")
});
```

### Déclarer le plugin

Maintenant que la configuration du « plugin » est effective nous devons le déclarer dans notre fichier `main.js` pour ça rien de compliquer :

ajouter l'import :

```
import "./plugins/vue2-leaflet";
```

🤓 Avec les autres import déjà existant.

### Questions

- Pourquoi vue2-leaflet et pas juste leaflet ?
- Quel est l'avantage ?

### Dépendance supplémentaire

Le gros avantage de NPM (et NodeJS) c'est la quantitié de librairie disponible pour répondre à un besoin, nous allons donc profiter de celle-ci pour gagner du temps dans notre réalisation.

Firebase est plutôt simple à utiliser, mais nativement celle-ci ne s'intégre pas directement avec le « state » d'un composant VueJS! Mais grace à d'excellent développeur c'est maintenant possible et très simplement. Pour ça nous allons utiliser :

- [Vuefire](https://github.com/vuejs/vuefire/tree/v1)

```bash
npm install vuefire --save
```

⚠️ Dans une prochaine étape nous allons configurer vuefire. Pour l'instant le package est disponible mais non actif.

🤓 Je vous invite quand même à aller voir [la documentation](https://github.com/vuejs/vuefire/tree/v1) de VueFire pour voir de quoi il en retourne !

## Création du projet sur Firebase

Maintenant que nos dépendances sont installés et que notre projet est initialisé, nous allons configurer le projet sur Firebase :

Première étape [créer le projet sur le site de Firebase](https://console.firebase.google.com/u/0/)

![Création Firebase](./ressources/creation-firebase.png)

Maintenant que le projet est créé, nous allons récupérer la configuration :

![Configuration Web](./ressources/configuration-web.png)

Nous allons récupérer une partie du code fourni… Nous allons prendre la configuration (dans mon cas)

```js
// Initialize Firebase
var config = {
  apiKey: "✋-CHANGE-CHANGE-CHANGE-CHANGE-✋",
  authDomain: "reatlime-maps.firebaseapp.com",
  databaseURL: "https://reatlime-maps.firebaseio.com",
  projectId: "reatlime-maps",
  storageBucket: "reatlime-maps.appspot.com",
  messagingSenderId: "✋✋✋✋✋✋✋✋"
};

export default config;
```

Nous allons mettre le code dans le fichier `src/config/firebase.js` ⬅️

⚠️ ✋ Attention à bien changer la valeur de `apiKey` et `messagingSenderId`. ✋ ⚠️

BRAVO ! Votre projet est maintenant capable de « se connecter » avec Firebase !

### Questions

- Et la sécurité ? À votre avis comment ça fonctionne ?
- Est-il possible de faire autrement ?

## Modification du code pour inclure la configuration Firebase

Maintenant que nous avons ajouté la configuration, nous devons la déclarer dans notre code. Comme pour Vue2-Leaflet nous allons ajouter un fichier de « configuration du plugins » dans le dossiers `src/plugins/` ajouter un fichié nommé `firebase.js` avec le contenu suivant

```js
import firebaseConfig from "../config/firebase";
import firebase from "firebase/app";
firebase.initializeApp(firebaseConfig);
```

Comme pour leaflet, ajouter un import dans le fichier `main.js` pour référrencer notre « configuration de plugin » :

```js
import "./plugins/firebase";
```

### Questions

- Que fait le code ?
- Comment connaitre les autres options ?

## Testons

Bien maintenant, que nous avons mis en place les bases de notre projet, testons si celui-ci fonctionne correctement. Pour ça (dans un terminal) :

```bash
npm run serve
```

Après quelques secondes de compilation (pré-processing) vous devriez avoir sur votre écran :

![serve npm](./ressources/serve_npm.png)

Et dans votre navigateur toujours la même chose à savoir :

![VueJS init](./ressources/vuejs-init.png)

## Création de notre première vue / composant.

Notre projet est maintenant prêt à recevoir son premier `.vue` bien à vous. Toujours dans le but d'organiser sont travail nous allons commencer par créer un dossier :

- `src/views/`

Ce dossier nous servira à ranger l'ensemble de nos vues, pour l'instant nous allons créer une vue nommé `map.vue` ce fichier contiendra le code source de notre carte.

Créer le fichier `src/views/map.vue` avec le contenu suivant :

```vue
<template>
  <l-map id="map" :zoom="zoom" :center="center">
    <l-tile-layer :url="url"></l-tile-layer>
  </l-map>
</template>

<script>
import { LMap, LTileLayer, LMarker, LControl } from "vue2-leaflet";

export default {
  name: "myMap",
  data() {
    return {
      url: "http://{s}.tile.osm.org/{z}/{x}/{y}.png",
      zoom: 13,
      center: [47.472092, -0.550589]
    };
  },
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LControl
  },
  methods: {}
};
</script>

<style scoped>
#map {
  height: 100%;
  width: 100%;
}
</style>
```

✋ D'où vient le code ? Tout simplement une adaptation du [code de démonstration fourni par Vue2-Leaflet](https://korigan.github.io/Vue2Leaflet/#/components/l-map/)

## Utiliser notre premiere vue

Créer la vue ne déclenche rien, il faut maintenant l'importer. Comme vu en cours, la « base » de notre application est réparti entre deux fichiers :

- l'main.js : qui contient les imports de base et la déclaration de notre objet `.vue`.
- l'App.vue : qui contient la « racine » de notre HTML (c'est dans celui-ci que nous allons référencé notre nouvelle vue / composant)

Modifier le `App.vue` par :

```vue
<template>
  <myMap />
</template>

<script>
import myMap from "./view/map.vue";

export default {
  name: "app",
  components: {
    myMap
  }
};
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
</style>
```

### Questions

- Quels sont les différences ?
- Pourquoi le CSS n'est pas `scoped` ?
- À quoi correspond `components` ?

## Tester

Votre projet doit maintenant afficher une carte, tester rapidement via la commande :

```bash
npm run serve
```

![Première carte](./ressources/first-map.png)

## Configurer VueFire

Comme pour Vue2-Leaflet et firebase, vuefire nécéssite une déclaration pour être utilisé dans le projet.

- [Lire la documentation](https://github.com/vuejs/vuefire/tree/v1).
- Créer le fichier dans le dossiers `plugins`.
- Réaliser l'import dans le fichier `main.js`.

🤓 C'est la 3ème fois de ce TP que vous le faite, vous devez être capable de le faire de vous même.

{% reveal text="Voir la solution" %}

`src/plugins/vuefire.js`

```js
import Vue from "vue";
import VueFire from "vuefire";

Vue.use(VueFire);
```

`main.js`

```js
// […]
import "./plugins/vuefire";

// […]
```

{% endreveal %}

## TODO SUITE FIREBASE

## Amélioration 1 : centrer la carte sur votre position

Profitons des nouvelles fonctionnalités de nos navigateurs pour améliorer notre carte. Actuellement la carte est centrée sur Angers… C'est pratique… Si on ce trouve à Angers… dans tous les autres cas c'est pas forcément adapté. Nous allons donc utiliser l'API `geolocation` de notre navigateur.

Celle-ci permet de localiser une personne en fonction de sa connexion internet (ou GPS / Réseau téléphonique si disponible)

- [Documentation de l'API geolocation](https://developer.mozilla.org/en-US/docs/Web/API/Geolocation_API).
- Ajouter une méthode dasns le code dans le composant `map.vue`.
- La méthode doit mettre à jour le `this.center = [lat, lng]`.
- La méthode doit être appelé via un click utilisateur [Documentation de LControl](https://korigan.github.io/Vue2Leaflet/#/components/l-control/)

{% reveal text="Voir la solution" %}

template :
Dans le `l-map`

```html
<l-control position="bottomleft">
  <button @click="getUserLocation">Localiser moi</button>
</l-control>
```

methods :

```js
getUserLocation() {
      if ("geolocation" in navigator) {
        navigator.geolocation.getCurrentPosition(
          position => {
            this.center = [position.coords.latitude, position.coords.longitude];
          },
          error => {
            console.error(error);
          }
        );
      }
    }
```

{% endreveal %}
