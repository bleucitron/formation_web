# Modules

## À l'ancienne

On peut "importer" des scripts dans les HTML, via les balises `<script>`, soit en inline, soit en "script-src".

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="code1.js"></script>
    <script src="code2.js"></script>
    <script src="code3.js"></script>
    <script src="code4.js"></script>
    <script src="code5.js"></script>
    <script src="code6.js"></script>
  </head>
  <body></body>
</html>
```

---

## Dépendances explicites

Les différents morceaux de code d'une application dépendent les uns des autres. Mais en JavaScript, ces dépendances sont par défaut **implicites**.

On souhaite rendre claires les relations entre fichiers, afin de savoir sans équivoque quel fichier nécessite quels autres fichiers.

On veut donc rendre les dépendances entre fichiers **explicites**.

## Modules ES6

Quand on importe un module, on "récupère" ce que ce module exporte.

Le module "point d'entrée" n'exporte rien.

Les modules "feuilles" n'importent rien.

### [`export`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/export)

On peut exporter des valeurs, des objets, des fonctions...

```js
// export par défaut, n'a pas besoin de nom
export default { a: 1, b: 2 };

// marche aussi pour les fonctions
export default function () {
  console.log('Coucou');
}

export const maConst = 5; // export secondaire
```

### [`import`](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/import)

On peut importer depuis un module natif ou installé, ou depuis les fichiers locaux du projet.

```js
// un module importe d'autres modules

import monModule from 'monModule'; // import externe
import maFonction from './monFichierLocal'; // import local

import { pikachu, charmander as salameche } from 'pokemons'; // on importe seulement "pikachu" et "charmander", que je renomme en "salameche"

console.log(pikachu);

import * as pokemons from 'pokemons'; // on importe tous les exports

console.log(pokemons.pikachu);

// ...
```

**Les modules sont par défaut en mode strict !**

### Utiliser un module

Pour pouvoir utiliser un script de type module dans le HTML, il faut l'insérer dans un `<script>` de type `"module"`.

Toutes les dépendances d'un script `"module"` seront directement importées en suivant l'arbre de dépendances construit avec les différents `import` et `export`.

**Lorsque l'on utilise les modules, il faut impérativement servir sa page depuis un serveur HTTP (et non depuis le protocole `file://`).**

```html
<!DOCTYPE html>
<html>
  <head>
    <script src="code1.js" type="module"></script>
  </head>
  <body></body>
</html>
```

## Aller plus loin

Le développement web moderne s'appuie énormément sur le concept de "bundling", dont le principe est le suivant:

On "compile" tout le code en 1 seul (gros) fichier bien construit pour le charger dans le Html.

Pour mettre en place du bundling, il y a plusieurs alternatives disponibles.

- [`browserify`](http://browserify.org/)
- [`webpack`](https://webpack.js.org/)
- [`rollup`](https://rollupjs.org/guide/en)
- [`parcel`](https://parceljs.org/)

Ces outils nécessitent de travailler dans un environnement Node, puis de transformer le code Node en un code compatible navigateur.

Pour utiliser ces outils, il est donc nécessaire d'[installer Node](https://nodejs.org/en/) et un gestionnaire de paquets, [NPM](https://www.npmjs.com/) ou [Yarn](https://yarnpkg.com/en/).

Toutes ces techniques sortent largement du cadre de ce cours, mais sont intéressantes à étudier si l'on veut aller plus loin dans le développement web avec Javascript.
