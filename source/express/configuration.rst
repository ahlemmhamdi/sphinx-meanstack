.. _ex-configuration:

=====================================================================================
Express: configuration
=====================================================================================

**configuration**
_________________

Conditions préalables
----------------------

- Un environnement de développement local pour Node.js

Configuration du projet
------------------------

créez un nouveau répertoire de projet

.. code-block::

 mkdir express-example
..
accédez au répertoire nouvellement créé
.. code-block::

 cd express-example   
..
initialiser un nouveau projet npm
.. code-block::

 npm init -y    
..
installer le expresspackage
.. code-block::

 npm install express@4.17.1   
..
Création d'un serveur express
-----------------------------

.. code-block::

 const express = require('express');

 const app = express();   
.. 
La première ligne ici récupère le module Express principal du package que vous avez installé. Ce module est une fonction, 
que nous exécutons ensuite sur la deuxième ligne pour créer notre appvariable. Vous pouvez créer plusieurs applications 
de cette façon, chacune avec ses propres demandes et réponses.

.. code-block::

  const express = require('express');

 const app = express();

 app.get('/', (req, res) => {
  res.send('Successful response.');
 });  
..
c'est comment gérer une GETrequête adressée à notre serveur. Express inclut des fonctions similaires pour POST, PUT, etc
Ces fonctions prennent deux paramètres principaux. Le premier est l'URL sur laquelle cette fonction doit agir. 
Dans ce cas, nous ciblons '/', qui est la racine de notre site Web : dans ce cas, localhost:3000.

Le second paramètre est une fonction à deux arguments : req, et res. reqreprésente la requête qui a été envoyée au serveur ;
Nous pouvons utiliser cet objet pour lire des données sur ce que le client demande de faire. 
resreprésente la réponse que nous renverrons au client.

Ici, nous appelons une fonction sur res pour renvoyer une réponse : 'Successful response'

.. code-block::

 const express = require('express');

 const app = express();

 app.get('/', (req, res) => {
  res.send('Successful response.');
 });

 app.listen(3000, () => console.log('Example app is listening on port 3000.'));   
..
exécutez votre application :     
.. code-block::

  node server.js  
..
Ensuite, visitez localhost:3000 dans votre navigateur Web. La fenêtre de votre navigateur affichera : 'Successful response'. 
La fenêtre de votre terminal affichera : 'Example app is listening on port 3000'.

Utilisation du middleware
-------------------------

Pour définir une fonction middleware, nous appelons app.use()et lui transmettons une fonction. 
Voici une fonction intermédiaire de base pour imprimer l'heure actuelle dans la console lors de chaque requête :

..  code-block::

 const express = require('express');

 const app = express();

 app.use((req, res, next) => {
  console.log('Time: ', Date.now());
  next();
 });

 app.get('/', (req, res) => {
  res.send('Successful response.');
 });

 app.listen(3000, () => console.log('Example app is listening on port 3000.'));
..

next()appel indique au middleware d'aller à la fonction middleware suivante s'il y en a une.


transmettre un chemin au middleware, qui ne traitera que les requêtes vers cette route.
.. code-block::

 const express = require('express');

 const app = express();

 app.use((req, res, next) => {
  console.log('Time: ', Date.now());
  next();
 });

 app.use('/request-type', (req, res, next) => {
  console.log('Request type: ', req.method);
  next();
 });

 app.get('/', (req, res) => {
  res.send('Successful response.');
 });

 app.listen(3000, () => console.log('Example app is listening on port 3000.'));
..
exécutez votre application :
.. code-block::

  node server.js
..
Ensuite, visitez localhost:3000/request-typedans votre navigateur Web. 
La fenêtre de votre terminal affichera l'horodatage de la demande et 'Request type:  GET'.


Essayons maintenant d'utiliser le middleware existant pour servir les fichiers statiques.
Tout d'abord, dans le même dossier où se trouve le serveur express, créez un répertoire nommé publicet placez-y des fichiers.
Ensuite, installez le package serve-index:
.. code-block::

 npm install serve-index@1.9.1
..
Tout d'abord, importez le serve-indexpackage en haut du fichier du serveur.
Ensuite, incluez les middlewares express.staticet serveIndexet indiquez-leur 
le chemin d'accès depuis et le nom du répertoire :
.. code-block::

 const express = require('express');
 const serveIndex = require('serve-index');

 const app = express();

 app.use((req, res, next) => {
  console.log('Time: ', Date.now());
  next();
 });

 app.use('/request-type', (req, res, next) => {
  console.log('Request type: ', req.method);
  next();
 });

 app.use('/public', express.static('public'));
 app.use('/public', serveIndex('public'));

 app.get('/', (req, res) => {
  res.send('Successful response.');
 });

 app.listen(3000, () => console.log('Example app is listening on port 3000.'));
..
Maintenant, redémarrez votre serveur et accédez à localhost:3000/public. Une liste de tous vos fichiers vous sera présentée !


Ajouter le moteur de templating Handlebars et servir des fichiers HTML
-----------------------------------------------------------------------

Un moteur de templating permet de modifier dynamiquement le contenu de pages HTML du côté serveur.
Commencez par installer Handlebars avec npm dans le répertoire de votre projet :
.. code-block::

npm install express-handlebars
..

- Créez ensuite un nouveau dossier à la racine du répertoire de votre projet et nommez-le views” À l'intérieur de celui-ci, 
- créez un nouveau fichier appelé main.handlebars et deux sous-dossiers : layouts et partials.
- Les layouts forment la structure générale de la page ainsi que ses métadonnées. 
- Les partials sont des éléments qui peuvent être réutilisés sur plusieurs pages (par exemple, un menu). 
- Enfin, créez un nouveau fichier appelé index.handlebars dans le sous-dossier layouts.

Remplissez le fichier “index.handlebars” avec un code HTML basique tel que : 
.. code-block::

 <!DOCTYPE html>
 <html lang="fr">
 <head>
   <meta charset="utf-8" />
   <title>Mon application avec NodeJS, ExpressJS et Handlebars</title>
   <link rel="stylesheet" type="text/css" href="./style.css" />
 </head>
 <body>
   {{{body}}}
 </body>
 </html>
..
Notez que ce code contient une balise {{{body}}}. C’est ici que sera inséré dynamiquement le contenu de la page par handlebars.

Retournons au fichier index.js 
.. code-block::

 const handlebars = require('express-handlebars')
 app.set('view engine', 'handlebars')
..
Indiquez ensuite où se situe le répertoire contenant les layouts de votre application avec engine() :
.. code-block::

 app.engine('handlebars', handlebars({
    layoutsDir: __dirname + '/views/layouts',
 }))
..
Modifiez votre appel à la fonction get() pour servir le layout correspondant à la page demandée : 

.. code-block::

 app.get('/', function (req, res) {
   res.render('main', {layout : 'index'})
 })
..
dans main.handlebars
.. code-block::

 <h1>Contenu de Main</h1>
 <ul>
   <li>Element 1</li>
   <li>Element 2</li>
   <li>Element 3</li>
   <li>Element 4</li>
 </ul>
..
Enfin, permettons à l'application de charger un fichier css statique public avec :
.. code-block::

 h1{
   color:red
 }

 li{
   color:darkred
 }
..
dans index.js
.. code-block::

 const express = require('express')
 const app = express()

 const handlebars = require('express-handlebars')

 app.set('view engine', 'handlebars')
 app.engine('handlebars', handlebars({
    layoutsDir: __dirname + '/views/layouts',
 }))

 app.get('/', function (req, res) {
    res.render('main', {layout : 'index'})
 })

 app.use(express.static('public'))

 app.listen(3000, function () {
    console.log('Votre app est disponible sur localhost:3000 !')
 })

..

Générateur d'applications Express
---------------------------------

Utilisez l'outil de générateur d'applications, express, pour créer rapidement un squelette d'application.

Installez express à l'aide de la commande suivante :

.. code-block::

  npm install express-generator -g
..
Affichez les options de commande à l'aide de l'option -h :

.. code-block::

  express -h
..

Par exemple, ce code crée une application Express nomée myapp. L'application sera crée dans le dossier myapp, 
lui meme placé dans le repertoir de travail courant. Le moteur de vue sera configuré avec Pug:

.. code-block::

  express --view=pug myapp
..

Ensuite, installez les dépendances :

.. code-block::

  cd myapp
..
.. code-block::

  npm install
..
Sous MacOS ou Linux, exécutez l'application à l'aide de la commande suivante :

.. code-block::

  DEBUG=myapp:* npm start
..
Sous Windows, utilisez la commande suivante :

.. code-block::

  set DEBUG=myapp:* & npm start
..
Ensuite, chargez 'http://hôte_local:3000/'' dans votre navigateur pour accéder à l'application.


