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
