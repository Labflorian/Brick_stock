# BrickStock — règles du projet

BrickStock est une appli LEGO (stock de pièces, sets, minifigs) qui tient dans **un seul fichier `index.html`**.

## Règles (permanentes)

- **HTML/CSS/JS vanilla uniquement** : pas de framework, pas de `sw.js`, pas de PWA, pas de fichier supplémentaire obligatoire. Tout reste dans `index.html`.
- **Ne jamais casser** :
  - la synchro Gist (`createGist`, `pull`, `push`, `joinGist`) ;
  - le moteur de couleurs CIELAB (`rgbToLab`, `deltaE`, `colDist`, `analyseColor`) ;
  - les intégrations Rebrickable (`rb(...)`, clé `rbKey`) et Brickognize (`api.brickognize.com/predict/...`).
- **Pas de gestion d'emplacements physiques ni de bacs.**
- **Comportements automatiques** : le scan doit donner directement la bonne pièce. Pas d'étape manuelle supplémentaire par pièce.
- **Répondre en français.** Pour un gros changement, expliquer d'abord en quelques lignes ce qui va être fait.
- **Après chaque modification** : tester dans un navigateur (Playwright si possible) et vérifier qu'il n'y a **aucune erreur dans la console**.

## Git

- Dépôt GitHub : https://github.com/Labflorian/Brick_stock (remote `origin`).
- Site publié par GitHub Pages depuis `main` : https://labflorian.github.io/Brick_stock/
- On travaille sur `dev`. On ne fusionne dans `main` et on ne pousse `main` que sur accord explicite de l'utilisateur, puis on vérifie que le site en ligne sert la nouvelle version (sans erreur console).
- Le disque du Mac ne distingue pas les majuscules : ne jamais recréer `Index.html` à côté de `index.html`.
- Publier sans changer de branche localement : `git branch -f main dev && git push origin main`, puis attendre que https://labflorian.github.io/Brick_stock/ serve le nouveau fichier (~1 min) et vérifier la console.
- Le stock vit dans le localStorage du site et dans le Gist, pas dans index.html : avant de publier, vérifier que le diff ne touche pas aux clés de stockage ni à la synchro.

## Repères dans index.html

- `<head>` : petit script de thème, puis un gros `<style>`.
- Corps : `<header>`, modale Paramètres (Gist + API), modale sélecteur de couleur, onglets `#s-stock`, `#s-sets`, `#s-figs`, `#s-scan`, puis `<nav>`.
- Script principal (le plus long) : couleurs, stock, sets, synchro Gist, moteur CIELAB, caméra et scan.
- Ensuite, une série de blocs `<script>` ajoutés au fil des versions (v2, v3, v4, puis des correctifs ciblés). Plusieurs **remplacent ou enveloppent** des fonctions définies plus haut (ex. `renderPart`, `fetchEquivs`, `rowRes`). Avant de modifier une fonction, chercher si un bloc plus bas la redéfinit.
