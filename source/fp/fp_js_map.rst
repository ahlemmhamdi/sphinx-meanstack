.. _fp_js_map:

===========================================================
programmation fonctionnelle: Le pouvoir de map - importance 
===========================================================

**Le pouvoir de map**
____________________

qu'est-ce qu'un functor
-----------------------

est une relation qui existe entre deux ensembles de valeurs. Je sais que c'est vague, cela aura du sens dans une seconde. Disons que nous avons deux tableaux.


.. code-block::

 const favorite_numbers = [42, 69, 73];
 const increased_numbers = [43, 70, 74];
..

Imaginez que le tableau increment_numbers n'existe pas mais que nous avons toujours besoin de ces nombres, 
pour les faire réapparaître, tout ce dont nous avons besoin est notre bon vieil ami map .

.. code-block::

 const increased_numbers = favorite_numbers.map(num => num + 1);
..

map passera en revue chaque nombre, l'augmentera et le mettra dans un nouveau tableau qui ramènera increments_numbers 
à l'existence. Même si increased_numbers est quelque chose que nous avons fait, nous ne l'avons créé nulle part, 
nous n'avons pas inventé par magie 43 , 70 et 74 . Tout ce que nous avons fait était de décrire une relation 
entre ces nombres et nos favorite_numbers .


**Régles**
____________

Identité
----------

.. code-block::

 function identity(x) {
 return x;
 }
..

value et value.map(identity) doivent être équivalents.

.. code-block::

 [1,2,3];
 // => [1,2,3]
 [1,2,3].map(identity); // => [1,2,3]
..

si nous mappons un tableau de trois éléments, nous devons recevoir un nouveau tableau de trois éléments.


Composition
------------

si ona deux fonctions f(x) et g(x) 
value.map(fx).map(gx) et value.map(arg => gx(fx(arg))) doivent être équivalents.

.. code-block::

 function add_one(num) {
 return num + 1;
 }
 function times_two(num) {
 return num * 2;
 }
 [1].map(add_one).map(times_two);
 // => [4]
 [1].map(num => times_two(add_one(num))); // => [4]

..

  >>Il existe une autre structure populaire qui suit également les règles et c'est Promise .

.. code-block::

 // A value
 1;
 // A box
 Promise.resolve;
 // Look, a value in a box
 Promise.resolve(1);
 // Identity rule
 Promise.resolve(1).then(identity); // => 1 (in the future)
 // Composition
 Promise.resolve(1).then(add_one).then(times_two);
 // => 4
 Promise.resolve(1).then(num => times_two(add_one(num))); // => 4

..

Nous pouvons créer votre propre map en dehors de la structure.

.. code-block::

 const List = {
 map(fn, arr) {
 let result = [];
 for (let data of arr) {
 result.push(fn(data));
 }
 return result;
 }
 };

..

N'est-ce pas si mal. Et il fonctionne.

.. code-block::

 // Identity rule
 List.map(identity, [1]); // => [1]
 // Composition
 List.map(times_two, List.map(add_one, [1]));
 // => [4]
 List.map(num => times_two(add_one(num)), [1]); // => [4]

..

rien ne peut nous empêcher de faire la même chose avec des objets simples, car après tout,
les objets peuvent aussi contenir des ensembles de valeurs.

.. code-block::

 const Obj = {
 map(fn, ob) {
 let result = {};
 for (let [key, value] of Object.entries(ob)) {
 result[key] = fn(value);
 }
 return result;
 }
 };
 // Why stop at `map`?
 // Based on this you can also create a `filter` and `reduce`
 // Identity rule
 Obj.map(identity, {some: 1, prop: 2}); // => {some: 1, prop: 2}
 // Composition
 Obj.map(times_two, Obj.map(add_one, {some: 1, prop: 2})); // => {some: 4, prop: 6}
 Obj.map(num => times_two(add_one(num)), {some: 1, prop: 2}); // => {some: 4, prop: 6}
..

Exemple avec Stream
-------------------

.. code-block::

 // Set initial state
 const num_stream = Stream(0);
 // Create a dependent stream
 const increased = num_stream.map(add_one);
 // Get the value from a stream
 num_stream(); // => 0
 // Push a value to the stream
 num_stream(42); // => 42
 // The source stream updates
 num_stream(); // => 42
 // The dependent stream also updates
 increased(); // => 43
..

Commençons par la fonction getter et setter.

.. code-block::

 function Stream(state) {
 let stream = function(value) {
 // If we get an argument we update the state
 if(arguments.length > 0) {
 state = value;
 }
 // return current state
 return state;
 }
 return stream;
 }
..

.. code-block::

 // Initial state
 const num_stream = Stream(42);
 // Get state
 num_stream(); // => 42
 // Update
 num_stream(73);
 // Check
 num_stream(); // => 73
..


Commençons par la partie écouteur, 
nous voulons stocker un tableau d'écouteurs et exécuter chacun juste après le changement d'état.
.. code-block::

 function Stream(state) {
 +
 let listeners = [];
 +
 let stream = function(value) {
 if(arguments.length > 0) {
 state = value;
 +
 listeners.forEach(fn => fn(value));
 }
 return state;
 }
 return stream;
 }
..

Maintenant, nous allons utiliser la méthode de la carte, mais ce ne sera pas n'importe quelle méthode, 
nous devons suivre les règles:

Identité: lorsque la carte est appelée, elle doit préserver la forme de la structure. 
Cela signifie que nous devons retourner un nouveau flux.

Composition: appeler plusieurs fois la carte doit être équivalent à composer les rappels fournis à ces cartes. 

.. code-block::

 function Stream(state) {
 let listeners = [];
 let stream = function(value) {
 if(arguments.length > 0) {
 state = value;
 listeners.forEach(fn => fn(value));
 }
 return state;
 }
 stream.map = function(fn) {
 // Create new instance with transformed state.
 // This will execute the callback when calling `map`
 // this might not be what you want if you use a
 // function that has side effects. Just beware.
 let target = Stream(fn(state));
 // Transform the value and update stream
 const listener = value => target(fn(value));
 // Update the source listeners
 listeners.push(listener);
 return target;
 }
 return stream;
 }
..

Testons les règles. Nous commençons par l'identité.

.. code-block::

 // Streams are like a cascade
 // the first is the most important
 // this is the one that triggers all the listeners
 const num_stream = Stream(0);
 // Create dependent stream
 const identity_stream = num_stream.map(identity);
 // update the source
 num_stream(42);
 // Check
 num_stream();
 // => 42
 identity_stream(); // => 42
..

Vérifions maintenant la règle de composition.

.. code-block::

 // Create source stream
 const num_stream = Stream(0);
 // Create dependents
 const map_stream = num_stream.map(add_one).map(times_two);
 const composed_stream = num_stream.map(num => times_two(add_one(num)));
 // Update source
 num_stream(1);
 // Check
 map_stream();
 // => 4
 composed_stream(); // => 4
..


https://vonheikemen.github.io/devlog/web-development/learn-fp/the-power-of-map/