4.1 - TP cordova avancé : config.xml & plugins
==============================================

Objectif
--------
Savoir paramètrer une application cordova avec son fichier config.xml. Etre capable d'utiliser les fonctionnalités natives du périphérique avec les plugins.

Préparatifs
-----------
- créer un nouveau projet cordova 
- archiver/renommer le dossier `www` généré par cordova (ne pas le supprimer, nous aurons besoin de son contenu plus tard)
- placer le contenu du dossier `demarrage-es5` ou `demarrage-es6` (selon que vous souhaitez développer en ES6 ou en ES5) de ce repository dans un nouveau dossier `www` du projet

NB: si vous utilisez la version ES6, installez babel dans le dossier de votre projet
```bash
npm install --save-dev babel-cli babel-loader babel-core babel-preset-es2015
```
et compilez l'application avec la commande :
```bash
.\node_modules\.bin\babel www\js -d www\build --watch --source-maps
```

Instructions
------------
###1. adaptation du code fourni : passer d'une webapp à une app cordova
- reprendre la balise meta viewport du fichier index.html généré par cordova
- modifier le nouveau fichier index.html pour utiliser un fichier jquery local
- inclure cordova.js
- dans le main.js remplacer l'événement jquery "ready" par l'événement cordova "deviceready"


###2. optimisations
- forcer l'orientation portrait
- passer l'application en plein écran
- désactiver la couleur du tap en css (cf. CSS générée par Cordova)
- empêcher l'application de scroller
- utiliser les événements touchstart plutôt que click

###3. prendre l'utilisateur en photo au lancement du jeu
- installer le plugin Cordova permettant de manipuler la caméra
```bash
cordova plugin add cordova-plugin-camera
```
- lancer l'appareil photo à l'appui sur le bouton startgame
- afficher la photo dans le canvas (dans la fonction render)

###4. utiliser l'accéléromètre pour déplacer le joueur
- installer le plugin cordova permettant d'utiliser l'accéléromètre du device :
```bash
cordova plugin add cordova-plugin-device-motion
```
- utiliser la méthode watchAcceleration et inspecter les valeurs retournées
- modifier la position de l'image en fonction de l'accélération 


Pour aller plus loin
--------------------
- modifier le splash screen et l'icone de l'application avec les images de votre choix
- si vous avez réalisé la version ES5, faire la version ES6 du projet
- minifier et obfusquer le code JS généré, placer le code ES6 dans un dossier en dehors du www pour que les sources JS ne soient pas livrées dans l'application générée (apk, ipa, ...)
- gérer le multitouch pour détruire plusieurs monstres d'un coup
- détecter la collision entre le joueur et les monstres et détruire les monstres lorsque le joueur passe dessus.