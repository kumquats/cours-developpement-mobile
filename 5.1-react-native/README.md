# TP React Native

## Objectifs
Créer une application de recherche dans les articles wikipedia avec React Native. 

## Préparatifs
- ajouter la variable d'environnement ANDROID_HOME vers le dossier des sdk android
- vérifier la version de node et si nécessaire désinstaller et installer une version à jour
```bash
node -v
```
- mettre à jour npm 
```bash
npm install -g npm
```
- installer react-native-cli 
```bash
npm install -g react-native-cli
```
- créer un nouveau projet 
```bash
react-native init WikiReact
cd WikiReact
```
- lancer l'application et s'assurer que tout fonctionne
```bash
react-native run-android
```


## en cas de problème
- Le remote debugging via USB ne marche pas pour android < 5.0. Dans ce cas utiliser le debug via wifi
- en cas de soucis avec les versions de sdk, soit installer les sdk build tools demandés (solution recommandée) soit modifier ./android/app/build.gradle pour remplacer lignes 87 et 92 les valeurs de buildToolsVersion et targetSdkVersion pour correspondre aux build-tools et sdk installés
cf. http://stackoverflow.com/questions/33155087/react-native-on-android-failed-to-find-build-tools#34928913
- Dans le sdk manager : vérifier et installer/mettre à jour les `Extras > Android Support repository` cf. http://stackoverflow.com/questions/33023018/react-native-awesome-project-not-building-android-project#33023883

## Prise en main des outils de debug
- Afficher les outils de debug de l'app, en appuyant sur la touche "menu" du téléphone (ou appui long sur la touche "carré" sur android 6)
    + Activer le Live Reload
    + modifier le contenu du fichier index.android.js et constater le rechargement à chaud de l'appli
    + Activer la fonction "Debug JS Remotely"
    + ajouter un console.log dans le code et constater l'affichage dans la fenêtre de debug
    + inspecter le code JS et mettre un point d'arrêt. Recharger l'application et constater que l'exécution s'interromp au point d'arrêt
- télécharger react-native-debugger : https://github.com/jhen0409/react-native-debugger :
    + désactiver la fonction "Debug JS Remotely"
    + fermer l'onglet de debug de Chrome
    + fermer l'application mobile
    + dans un terminal sur le poste de développement, lancer la commande
    ```bash
    $ adb reverse tcp:8097 tcp:8097
    ```
    + lancer l'application react-native-debugger sur le poste de développement
    + lancer l'application sur le téléphone (en cliquant sur son icone)
    + activer la fonction "Debug JS Remotely"
    + modifier le texte de l'application
    + modifier la taille et la couleur du texte de l'application

## Instructions
- Créer un composant SearchForm contenant un texte arbitraire et l'afficher dans l'application.
- Modifier le composant SearchForm pour qu'il affiche sur la même ligne un champ de saisie (TextInput) et un bouton (Button ou TouchableOpacity/TouchableHighlight). Pour la mise en page se référer à https://facebook.github.io/react-native/docs/flexbox.html et https://facebook.github.io/react-native/docs/layout-props.html
- Détecter le clic sur le bouton submit du SearchForm et lancer une requête ajax vers l'api wikipedia (configurer la requête pour retourner 50 résultats - et non pas 10 par défaut - avec le paramètre GET `srlimit=50`) cf. https://www.mediawiki.org/wiki/API:Search
- Afficher un loading dans la page pendant le chargement
- Créer un composant permettant d'afficher les résultats de recherche avec pour chaque résultat son titre et son intro

## Pour aller plus loin
- Utiliser un composant [ListView](https://facebook.github.io/react-native/docs/listview.html) pour l'affichage des résultats. Constater la différence dans la gestion du scroll et la fluidité de l'application
- Détecter le tap sur un des résultats et afficher le détail
- Utiliser un composant [Navigator](https://facebook.github.io/react-native/docs/navigator.html) pour le passage de la page de liste à la page de détail