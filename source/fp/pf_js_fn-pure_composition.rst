.. _pf_js_fn-pure_composition:

===================================================================================================================================
programmation fonctionnelle:les effets secondaires et les fonctions pures en javascript -  Techniques de composition en javascript
===================================================================================================================================

**Traiter les effets secondaires et les fonctions pures en javascript**
________________________________________________________________________

fonction pures
--------------

une fonction pure est une fonction dont la sortie n'est déterminée que par son entrée et n'a aucun effet observable sur le monde extérieur.
si vous leur donnez les mêmes valeurs d'entrée, ils vous renverront toujours la même sortie.ceci un exemple:
Celui-ci est pur.

.. code-block::

 function increment(number) {

 return number + 1;

 }
..

Celui-ci n'est pas

..code-block::

 Math.random();

..

Effets secondaires
-------------------

J'appellerai effet secondaire tout ce qui compromet la pureté d'une fonction. La liste comprend, sans s'y limiter:
Changer (muter) une variable externe de quelque manière que ce soit.
Afficher des choses à l'écran.
Écriture dans un fichier.
Faire une requête http.
Générez un processus.
Sauvegarde des données dans une base de données.
Appeler d'autres fonctions avec des effets secondaires.
Manipulation du DOM.
L'aléatoire.
Ainsi, toute action qui peut changer « l'état du monde » est un effet secondaire.

Une autre façon de le dire sera : la bonne vieille séparation des préoccupations. 
C'est la manière non compliquée. S'il existe un moyen de séparer un calcul d'un effet secondaire, 
placez le calcul sur une fonction et donnez la sortie à la fonction/au bloc qui a l'effet secondaire.

- Cela pourrait être aussi simple que de faire quelque chose comme ça

.. code-block::

 function some_process() {
 const data = get_data_somehow();
 const clean_data = computation(data);
 const result = save(clean_data);
 return result;
}
..

Maintenant, some_process n'est toujours pas pur mais ça va, nous écrivons du javascript,
nous n'avons pas besoin que tout soit pur, ce dont nous avons besoin c'est de garder notre raison. 
En séparant les effets secondaires du calcul pur, nous avons créé trois fonctions indépendantes qui résolvent un seul problème à la fois.
Vous pouvez même aller plus loin et utiliser une fonction d'assistance comme pipe pour vous débarrasser de ces variables intermédiaires et composer ces fonctions directement.

.. code-block::

 const some_process = pipe(get_data_somehow, computation, save);
..

Faire en sorte que quelqu'un d'autre s'occupe du problème
----------------------------------------------------------

Comme nous le savons tous, la vie n'est pas toujours aussi simple,
parfois nous ne pouvons tout simplement pas créer ce joli pipeline de fonctions.
Dans certaines situations, nous devons créer des effets secondaires au milieu d'un processus et lorsque cela se produit,
nous pouvons toujours tricher. En javascript, nous pouvons traiter les fonctions comme des valeurs, 
ce qui nous permet de faire des choses amusantes comme transmettre des fonctions en tant que paramètres à d'autres fonctions. De cette façon, la fonction peut avoir le

.. code-block::

 function transform(onchange, data) {
 let result = Array.isArray(data) ? [] : {};
 for(let key in data) {
 result[key] = data[key] + 1;
 onchange(data[key], result[key]);
 }
 return result;
 }
..

Effets paresseux
------------------
L'idée ici est de retarder l'inévitable. Au lieu d'effectuer l'effet secondaire tout de suite,
vous fournissez un moyen à l'appelant de votre fonction d'exécuter l'effet secondaire quand il le souhaite. 
Vous pouvez le faire de plusieurs manières.

1. Utilisation de function wrappers

Comme je l'ai déjà mentionné en javascript, vous pouvez traiter les fonctions comme des valeurs 
et une chose que vous pouvez faire avec les valeurs est de les renvoyer à partir de fonctions. 
Je parle de fonctions qui renvoient des fonctions. Combien de fois avez-vous vu quelque chose comme ça ?

..code-block::

 function Stuff(thing) {
 // setup
 return {
 some_method() {
 // code...
 },
 other() {
 // code...
 }
 }
 }
..

Est une fonction régulière qui renvoie un objet, et nous savons tous que les objets peuvent avoir des méthodes. 
Ce que nous voulons faire est un peu comme ça, nous voulons convertir le bloc qui contient l'effet secondaire 
en une fonction et le retourner.

..code-block::

 function some_process(config) {
 /*
 * do some pure computation with config
 */
 return function _effect() {
 /*
 * do whatever you want in here
 */
 }
 }
..

De cette façon, nous donnons à l'appelant de notre fonction la possibilité d'utiliser l'effet secondaire 
quand il le souhaite, et il peut même le transmettre et le composer avec d'autres fonctions. 
Il est intéressant de noter que ce modèle n'est pas très courant, peut-être parce qu'il existe 
d'autres moyens d'atteindre le même objectif.

2. Utiliser des structures de données

Une autre façon de créer des effets paresseux consiste à envelopper un effet secondaire dans une structure de données. 
Ce que nous voulons faire, c'est traiter nos effets comme des données régulières, avoir la possibilité de les manipuler 
et même d'enchaîner d'autres effets de manière sûre (je veux dire sans les exécuter). 
Jetez un œil à ce code qui utilise rxjs.

.. code-block::

 // taken from:
 // https://www.learnrxjs.io/operators/creation/create.html
 /*
 Increment value every 1s, emit even numbers.
 */
 const evenNumbers = Observable.create(function(observer) {
 let value = 0;
 const interval = setInterval(() => {
 if (value % 2 === 0) {
 observer.next(value);
 }
 value++;
 }, 1000);
 return () => clearInterval(interval);
 });
..


Le résultat de Observable.create retarde non seulement l'exécution de setInterval, mais vous donne également
la possibilité d'appeler evenNumbers.pipe pour enchaîner d'autres observables qui peuvent
également avoir d'autres effets secondaires.
Maintenant, bien sûr, les observables et les rxjs ne sont pas le seul moyen, nous pouvons créer notre propre type d'effet. 
Si nous voulons en créer un, nous n'avons besoin que d'une fonction pour exécuter l'effet et d'une autre qui nous permette 
de composer des effets.


.. code-block::

 function Effect(effect) {
 return {
 run(...args) {
 return effect(...args);
 },
 map(fn) {
 return Effect(arg => fn(effect(arg)));
 }
 };
 }
..

Cela peut ne pas sembler grand-chose, mais c'est en fait assez pour être utile. 
Vous pouvez commencer à composer vos effets sans déclencher aucune modification de l'environnement. 
Vous pouvez maintenant faire des choses comme ça.

.. code-block::

 const persist = (data) => {
 console.log(`saving ${data} to a database...`);
 return data.length ? true : false;
 };
 const show_message = result => result
 ? console.log('we good')
 : console.log('we not good');
 const save = Effect(persist).map(show_message);
 save.run('some stuff');
 // saving some stuff to a database...
 // we good
 save.run('');
 // saving to a database...
 // we not good
..

Si vous avez utilisé Array.map pour composer des transformations de données, 
vous vous sentirez comme chez vous lorsque vous utiliserez Effect , 
tout ce que vous avez à faire est de fournir les fonctions avec l'effet secondaire et à la fin de la chaîne, 
l'effet résultant saura quoi faire quand vous êtes prêt à l'appeler. 
Je n'ai fait qu'effleurer la surface de ce que vous pouvez faire avec Effect , 
si vous voulez en savoir plus, essayez de rechercher le terme foncteur et IO Monad , 
je vous promets que ça va être amusant.


  >>Maintenant, vous cliquez sur le lien à la fin de l'article, c'est un très bon article.

  https://vonheikemen.github.io/devlog/web-development/learn-fp/dealing-with-side-effects-and-pure-functions/


**programmation fonctionnellepour Javascript : Techniques de composition**
__________________________________________________________________________

Qu'est-ce que la composition fonctionnelle ?
C'est un mécanisme qui nous permet de combiner deux ou plusieurs fonctions en une nouvelle fonction. 
Cela ressemble à une idée simple, n'avons-nous pas tous, à un moment de notre vie, combiné quelques fonctions ? 
Mais pensons-nous vraiment à la composition lorsque nous les créons ? 
Qu'est-ce qui va nous aider à faire des fonctions déjà conçues pour être combinées ?

Philosophie
------------
La composition des fonctions est plus efficace si vous suivez certains principes.
La fonction ne doit avoir qu'un seul but, une seule responsabilité.
Pensez toujours que la valeur renvoyée sera consommée par une autre fonction.

C'est le fichier.

.. code-block::

 ENV=development
 HOST=http://locahost:5000
..

Pour afficher le contenu du fichier à l'écran, nous utilisons cat .

.. code-block::

 cat .env
..

Pour filtrer ce contenu et rechercher la ligne que nous voulons, nous utilisons grep , 
fournissons le modèle de la chose que nous voulons et le contenu du fichier.

.. code-block::

 cat .env | grep "HOST=.*"
..

Pour obtenir la valeur que nous utilisons cut , cela va prendre le résultat fourni par grep et le diviser à l'aide d'un délimiteur, 
puis cela nous donnera la section de la chaîne que nous lui disons.

.. code-block::

 cat .env | grep "HOST=.*" | cut --delimiter="=" --fields=2
..

Cela devrait nous donner.

.. code-block::

 http://locahost:5000
..

Si nous mettons cette chaîne de commandes dans un script ou une fonction à l'intérieur de notre .bashrc, 
nous aurons effectivement une commande qui peut être utilisée de la même manière par d'autres commandes 
que nous ne connaissons même pas.C'est le genre de flexibilité et de pouvoir que nous voulons avoir.


Les fonctions sont des choses
-----------------------------


Retournons-nous et portons notre attention sur javascript. Avez-vous déjà entendu l'expression «fonction de première classe»?
Cela signifie que les fonctions peuvent être traitées comme n'importe quelle autre valeur. Comparons avec des tableaux.
Vous pouvez les affecter à des variables

.. code-block::

 const numbers = ['99', '104'];
 const repeat_twice = function(str) {
 return str.repeat(2);
 };
..

Pass them around as arguments to a function

.. code-block::

 function map(fn, array) {
 return array.map(fn);
 }
 map(repeat_twice, numbers);
..

Return them from other functions

.. code-block::

 function unary(fn) {
 return function(arg) {
 return fn(arg);
 }
 }
 const safer_parseint = unary(parseInt);
 map(safer_parseint, numbers);
..

Composition in practice
-----------------------

Obtenez le contenu du fichier.

.. code-block::

 const fs = require('fs');
 fonction get_env() {
 return fs.readFileSync('.env', 'utf-8');
 }
..

Obtenez la valeur.

.. code-block::

 function get_value(str) {
 return str.split('=')[1];
 }
..

Natural composition
-------------------

.. code-block::

 get_value(search_host(get_env()));
..

C'est la configuration parfaite pour la composition de fonctions, la sortie d'une fonction devient l'entrée de la suivante

.. code-block::

 test(ping(get_value(search_host(get_env()))));
..

Composition automatique
-----------------------


C'est là que nos nouvelles connaissances sur les fonctions commencent à être utiles. 
Pour résoudre notre problème de parenthèse, nous allons "automatiser" les appels de fonction, 
nous allons créer une fonction qui prend une liste de fonctions, les appelle une par une et s'assure 
que la sortie de l'une devient l'entrée de la suivante.

.. code-block::

 function compose(...fns) {
 return function _composed(...args) {
 // Index of the last function
 let last = fns.length - 1;
 // Call the last function
 // with arguments of `_composed`
 let current_value = fns[last--](...args);
 // loop through the rest in the opposite direction
 for (let i = last; i >= 0; i--) {
 current_value = fns[i](current_value);
 }
 return current_value;
 };
 }
..

Maintenant, nous pouvons le faire.

.. code-block::

 const get_host = compose(get_value, search_host, get_env);
 // get_host is `_composed`
 get_host();
..

Notre problème de parenthèse a disparu, nous pouvons ajouter plus de fonctions sans nuire à la lisibilité.

Fonctions avec plusieurs entrées
--------------------------------

La solution à cela est une application partielle et heureusement pour nous, 
javascript a un excellent support pour les choses que nous voulons faire. 
Notre objectif est simple, nous allons passer certains des paramètres dont une fonction a besoin mais
sans l'appeler. Nous voulons pouvoir le faire.

..code-block::

 const get_host = pipe(
 cat,
 grep('^HOST='),
 cut({ delimiter: '=', fields: 2 })
 );
 get_host('.env');
..

Pour rendre cela possible nous allons faire du currying, cela consiste à transformer une fonction à plusieurs paramètres 
en plusieurs fonctions à un seul paramètre. Pour ce faire, nous prenons un paramètre à la fois, continuons simplement à 
renvoyer des fonctions jusqu'à ce que nous obtenions tout ce dont nous avons besoin. Nous allons le faire pour grep et cut.

.. code-block::

 - function grep(pattern, content) {
 + function grep(pattern) {
 +
 return function(content) {
 const exp = new RegExp(pattern);
 const lines = content.split('\n');
 return lines.find(line => exp.test(line));
 +
 }
 }
 - function cut({ delimiter, fields }, str) {
 + function cut({ delimiter, fields }) {
 +
 return function(str) {
 return str.split(delimiter)[fields - 1];
 +
 }
 }
..

Functions with multiple outputs
-------------------------------

Plusieurs sorties ? Je veux dire les fonctions dont la valeur de retour peut avoir plus d'un type. 
Cela se produit lorsque nous avons des fonctions qui répondent différemment selon la façon dont 
nous les utilisons ou dans quel contexte.

.. code-block::

 function cat(filepath) {
 return fs.readFileSync(filepath, 'utf-8');
 }
..

Dans cat, nous avons readFileSync , c'est celui qui lit le fichier dans notre système, 
une action qui peut échouer pour de nombreuses raisons.
Cela signifie que cat peut renvoyer une chaîne si tout se passe bien, 
mais peut également générer une erreur si quelque chose ne va pas. Nous devons gérer les deux cas.
Malheureusement pour nous, les exceptions ne sont pas la seule chose dont nous devons nous soucier, 
nous devons également faire face à l'absence de valeurs. Dans grep, nous avons cette ligne.

.. code-block::

 lines.find(line => exp.test(line));
..

La méthode find est celle qui évalue chaque ligne du fichier. Contrairement à readFileSync , find ne renvoie pas d'erreur, 
il renvoie simplement undefined . Ce n'est pas comme si indéfini était mauvais, c'est que nous n'en avons aucune utilité. 
En supposant que le résultat sera toujours une chaîne, c'est ce qui peut provoquer une erreur.
Comment gère-t-on tout cela ?
Functors && Monads (désolé pour les gros mots). Donner une explication appropriée de ces deux-là prendrait trop de temps, 
nous allons donc nous concentrer uniquement sur les aspects pratiques. Pour le moment tu peux
Considérez-les comme des types de données qui doivent obéir à certaines lois . Où allons-nous commencer? Avec des foncteurs.

.. code-block::

 const add_one = num => num + 1;
 const number = [41];
 const empty = [];
 number.map(add_one); // => [42]
 empty.map(add_one); // => []
..


https://vonheikemen.github.io/devlog/web-development/learn-fp/composition-techniques/

