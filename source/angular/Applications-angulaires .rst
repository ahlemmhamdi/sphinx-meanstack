
.. _application-an:

===========================================================
Angular: Applications Angular : L'essentiel
===========================================================

**Applications Angular : L'essentiel**
______________________________________


Cette section explique les idées de base derrière Angular. Comprendre ces idées peut vous aider à concevoir et 
à créer vos applications plus efficacement.

Composants
----------

.. code-block::

 import { Component } from '@angular/core';

 @Component({
  selector: 'hello-world',
  template: `
    <h2>Hello World</h2>
    <p>This is my first component!</p>
  `
 })
 export class HelloWorldComponent {
  // The code in this class drives the component's behavior.
 }
..

Pour utiliser ce composant, vous écrivez ce qui suit dans un modèle :

.. code-block::

 <hello-world></hello-world>
..   

Lorsque Angular rend ce composant, le DOM résultant ressemble à ceci :

.. code-block::

  <hello-world>
    <h2>Hello World</h2>
    <p>This is my first component!</p>
  </hello-world>  
.. 

Modèles
-------

Chaque composant a un modèle HTML qui déclare le rendu de ce composant. Vous définissez ce modèle soit en ligne, 
soit par chemin de fichier.

Angular étend HTML avec une syntaxe supplémentaire qui vous permet d'insérer des valeurs dynamiques à partir de votre 
composant. Angular met automatiquement à jour le DOM rendu lorsque l'état de votre composant change. Une application de 
cette fonctionnalité consiste à insérer du texte dynamique, comme illustré dans l'exemple suivant.


.. code-block::

   <p>{{ message }}</p> 
..

La valeur de message provient de la classe de composant :  

.. code-block::

 import { Component } from '@angular/core';

  @Component ({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
  })
  export class HelloWorldInterpolationComponent {
    message = 'Hello, World!';
  }  
..

Lorsque l'application charge le composant et son modèle, l'utilisateur voit ce qui suit :

.. code-block::

    <p>Hello, World!</p>

..
Angular prend également en charge les liaisons de propriétés, pour vous aider à définir des valeurs pour les propriétés 
et les attributs des éléments HTML et à transmettre des valeurs à la logique de présentation de votre application.

.. code-block::

 <p
  [id]="sayHelloId"
  [style.color]="fontColor">
  You can set my color in the component!
 </p>
..
Déclarez les écouteurs d'événement pour écouter et répondre aux actions de l'utilisateur telles que les frappes, 
les mouvements de la souris, les clics et les touchers. Vous déclarez un écouteur d'événement en spécifiant le nom 
de l'événement entre parenthèses :

.. code-block::

 <button
  [disabled]="canClick"
  (click)="sayMessage()">
  Trigger alert message
 </button>
..
L'exemple précédent appelle une méthode, qui est définie dans la classe de composant :
.. code-block::

  sayMessage() {
  alert(this.message);
  }
..              

un exemple combiné d'interpolation
----------------------------------

liaison de propriété et  d'événement dans un modèle angular :

.. code-block::

 import { Component } from '@angular/core';
 
 @Component ({
  selector: 'hello-world-bindings',
  templateUrl: './hello-world-bindings.component.html'
 })
 export class HelloWorldBindingsComponent {
  fontColor = 'blue';
  sayHelloId = 1;
  canClick = false;
  message = 'Hello, World';
 
  sayMessage() {
    alert(this.message);
  }
 
 }
..
Le code suivant est un exemple de la directive.*ngIf
.. code-block::
 import { Component } from '@angular/core';
 
 @Component({
  selector: 'hello-world-ngif',
  templateUrl: './hello-world-ngif.component.html'
 })
 export class HelloWorldNgIfComponent {
  message = 'I\'m read only!';
  canEdit = false;
 
 onEditClick() {
    this.canEdit = !this.canEdit;
    if (this.canEdit) {
      this.message = 'You can edit me!';
    } else {
      this.message = 'I\'m read only!';
    }
  }
 } 
..
    
Injection de dépendance   
-----------------------

Pour illustrer le fonctionnement de l'injection de dépendance, considérons l'exemple suivant. Le premier fichier, 
logger.service.ts, définit une Loggerclasse. Cette classe contient une writeCountfonction qui enregistre un numéro 
dans la console.

.. code-block::
    
 import { Injectable } from '@angular/core';

 @Injectable({providedIn: 'root'})
 export class Logger {
  writeCount(count: number) {
    console.warn(count);
  }
 }    
..

Ensuite, le hello-world-di.component.tsfichier définit un composant angulaire. Ce composant contient un bouton qui utilise 
la writeCountfonction de la classe Logger. Pour accéder à cette fonction, le Loggerservice est injecté dans la 
HelloWorldDIclasse en l'ajoutant private logger: Loggerau constructeur.  
.. code-block::

 import { Component } from '@angular/core';
 import { Logger } from '../logger.service';

 @Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
 })
 export class HelloWorldDependencyInjectionComponent  {
  count = 0;

  constructor(private logger: Logger) { }

  onLogMe() {
    this.logger.writeCount(this.count);
    this.count++;
  }
 }    
..
