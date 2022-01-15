.. _ex-introduction:

=====================================================================================
Express: Qu'est-ce qu'Express - Exemple - pourquoi Express - Historique
=====================================================================================

**Qu'est-ce qu'Express**
__________________________

Express.js est un framework pour construire des applications web basées sur Node.js. 
C'est de fait le framework standard pour le développement de serveur en Node.js. 

**Exemple**
___________

Le code JavaScript ci-dessous démarre un serveur Web à l'écoute sur le port 3000

.. code-block::

 const express = require("express");
 const app = express();

 app.get('/', (req, res) => res.send('Hello, World!'))

 app.listen(3000, () => {
 console.log('Serveur en écoute sur le port 3000')
 });
..
**pourquoi Express**
___________________

Il est utilisé pour concevoir et créer des applications Web rapidement et facilement. 
Les applications Web sont des applications Web que vous pouvez exécuter sur un navigateur Web. Depuis Express. 
js ne nécessite que javascript, il devient plus facile pour les programmeurs et les développeurs de créer des applications 
Web et des API sans aucun effort.

**Historique**
_______________

- le 22 mai 2010: la Version 0.12: a été fondé par TJ Holowaychuk. 
- En juin 2014: les droits de gestion du projet ont été acquis par StrongLoop . 
- Septembre 2015: StrongLoop a été acquis par IBM
- Janvier 2016, IBM a annoncé qu'il placerait Express.js sous la direction de l'incubateur Node.js Foundation.

