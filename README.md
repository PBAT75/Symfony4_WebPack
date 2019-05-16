# Symfony 4 - Installation de WebPack Encore
- Installation via Flex:
```composer require encore```
- Installer le JS avec npm:
```npm install```
- Modifier le fichier de configuration webpack.config.js:
    - Décommenter la ligne pour activer le SassLoader: `.enableSassLoader()`
        
- Installer les dépendance dont webpack à besoin ainsi que BootStrap et FontAwesome et jQuery<br>
```npm install sass-loader node-sass bootstrap jquery @fortawesome/fontawesome-free popper.js --save-dev```

- Dans le fichier assets/js/apps.js:
    - modifier la ligne `require('../css/app.css');` en `require('../css/app.scss');`
    - Décommenter `const $ = require('jquery');`
    - Ajouter en dessous: `require('bootstrap');`<br>
    *A savoir: En important bootstrap, il va initaliser<br>`const $ = require('jquery');`*
    
    - Supprimer la ligne de console.log()
    
- Renommer le fichier `assets/css/app.css` en `assets/css/app.scss`

- Dans le fichier `assets/js/app.scss` ajouter les lignes suivantes pour chager bootstrap et fontawesome:
```
//BOOTSTRAP
@import "~bootstrap/scss/bootstrap";

// FONTAWESOME
@import "~@fortawesome/fontawesome-free/css/all";
```

- Supprimer le backdround du body dans le fichier scss
- Lancer la commande `npm run dev` pour compiler les fichiers
- Aller dans `base.html.twig` (*qui, pour la future nouvelle bonne pratique doit être renommé en layout.html.twig*)
- Modifier le block stylesheets comme suit:
```
{% block stylesheets %}
    {# 'app' must match the first argument to addEntry() in webpack.config.js #}
    {{ encore_entry_link_tags('app') }}

    <!-- Renders a link tag (if your module requires any CSS)
    <link rel="stylesheet" href="/build/app.css"> -->
{% endblock %}
```
- Modifier le block javascript comme suit:
```
{% block javascripts %}
    {{ encore_entry_script_tags('app') }}

    <!-- Renders app.js & a webpack runtime.js file
        <script src="/build/runtime.js"></script>
        <script src="/build/app.js"></script> -->
{% endblock %}
```
- **Ici il y a quelque chose de nouveau !**<br>
WebPack à besoin du fichier `runtime.js` pour se charger correctement (et initialiser les dépendances). `encore_entry_script_tags()` se charge de faire en sorte que le `runtime.js` soit chargé 1 seule fois, ainsi que le fichier JS ou CSS.

## EN CAS DE PROBLEME AVEC jQUERY:
- Décommenter la ligne fixer jQuery: `.autoProvidejQuery()`
- Ajouter en dessous: `global.$ = global.jQuery = $;`
