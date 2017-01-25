3.1 - TP cordova : build, tests, premières apps
===============================================

Objectif
--------
Créer un nouveau projet cordova, utiliser les différentes méthodes de déploiement, et les principaux outils de test et debug. Créer une première single page app.

Exercices
---------
## 0. Installation
- installer le sdk android en suivant les instructions du support
- installer la CLI Cordova et PhoneGap 

## 1. Création d'un projet
- dans un terminal lancer les commandes suivantes
```
cordova create bazinga fr.kumquats.bazinga Bazinga
cd bazinga
cordova platform add android
```

## 2. Tester sur l'emulateur
```
cordova emulate android
```

## 3. Test sur un périphérique connecté
- activer les options développeur et autoriser le débogage usb sur le téléphone
- installer le driver USB propre au téléphone
- connecter le téléphone au PC avec le cable USB
- lancer la commande : ```adb devices```. Cela doit afficher une demande  une autorisation sur le téléphone puis, après acceptation, afficher l'id du périphérique suivi de "device" dans la console
- déployer le projet sur le téléphone connecté : 
````
cordova run android --device
````

## 3b. Debug avec chrome dev tools (android 4.4 mini)
- ouvrir dans Chrome (côté poste de développement) l'adresse : chrome://inspect

## 4. Installer l'apk depuis une URL
- sur le poste de développement :
    + ```cordova build android```
    + copier l'apk généré depuis le dossier platforms/android/build/outputs/apk/
    + coller l'apk dans le répertoire web racine de votre serveur apache (ex. c:/xampp/htdocs)
- sur le téléphone : 
    + autoriser l'installation de sources inconnues (settings>security)
    + lancer Chrome et aller sur l'adresse du poste de développement pour télécharger le fichier apk (http://192.168.xxxxx/bazinga.apk)

## 5. Debug avec Phonegap Developer app
- *facultatif selon les installations : dans le fichier index.html commenter la ligne ```<meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: https://ssl.gstatic.com 'unsafe-eval'; style-src 'self' 'unsafe-inline'; media-src *">```*
- connecter le téléphone et le poste de développement au même réseau wifi (hotspot si nécessaire)
- installer Phonegap Developer App sur le téléphone depuis le store (iOS, Android ou Windows)
- dans le dossier du projet lancer la commande : 
```
phonegap serve
```
- lancer PhoneGap Developer App sur le téléphone
- entrer l'url affichée dans la ligne de commande > L'application se lance dans le téléphone
- en cas de soucis, creer un dossier/fichier : ```.cordova/config.json```
- modifier les fichiers html/css/js et voir l'effet du live reload de l'app

NB : on peut voir les console.log dans la ligne de commande

NB : plusieurs devices peuvent se connecter au même serveur

## 6. Build du projet avec phonegap-build
- créer un compte sur https://build.phonegap.com/
- compiler l'applicatio en uploadant un zip contenant le fichier config.xml et le dossier www 
- scanner le QRCode généré par PhoneGap build avec le téléphone, l'application doit se télécharger. Installer l'apk ainsi téléchargé.

## 8. Créer une application multi-pages :
- ajouter un fichier `page2.html` dans le dossier `www`
- ajouter un lien dans la page `index.html` vers ce `page2.html` (chemin relatif)
- recompiler l'application pour voir le résultat

## 9. Créer une première SPA :
- supprimer le fichier page2.html
- en javascript, détecter le clic sur le lien et modifier le DOM pour afficher le contenu de la page2 à la place de l'index

## 10. Portage d'une web app
- Créer un nouveau projet et y placer les fichiers du TP "wikisearch"
- adapter le code pour se passer du fichier `proxy.php` pour interroger directement l'API wikipedia
    + lors de la recherche, lancer un appel ajax vers 
    https://fr.wikipedia.org/w/api.php?action=query&format=json&list=search&srsearch=<marecherche>
    + lors du clic sur un résultat de recherche, lancer un appel ajax vers :
    https://fr.wikipedia.org/w/api.php?action=query&format=json&prop=revisions&rvprop=content&titles=<titredelapage>