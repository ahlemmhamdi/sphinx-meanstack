.. _directives:

================================================
Angular: directives - Injection de dépendances 
================================================



**Directives**
_____________


Les différents types de directives angulaires sont les suivants :

1. Composants : directives avec un modèle. Ce type de directive est le type de directive le plus courant.
2. Directives d' attribut : directives qui modifient l'apparence ou le comportement d'un élément, d'un composant ou d'une autre directive.
3. Directives structurelles : directives qui modifient la disposition du DOM en ajoutant et en supprimant des éléments DOM.

**Directives d'attributs intégrées**
____________________________________

Les directives d'attribut écoutent et modifient le comportement d'autres éléments, attributs, propriétés et composants HTML.
Les directives d'attribut les plus courantes sont les suivantes :

- NgClass—ajoute et supprime un ensemble de classes CSS.
- NgStyle—ajoute et supprime un ensemble de styles HTML.
- NgModel: ajoute une liaison de données bidirectionnelle à un élément de formulaire HTML.

**Ajouter et supprimer des classes avec NgClass**
-------------------------------------------------
Utilisation NgClass avec une expression
----------------------------------------
Sur l'élément que vous souhaitez styliser, ajoutez -le et définissez-le égal à une expression.
.. code-block::

    <!-- toggle the "special" class on/off with a property -->
   <div [ngClass]="isSpecial ? 'special' : ''">This div is special</div>
..
Utilisation NgClass avec une méthode
-----------------------------------
Pour l'utiliser NgClassavec une méthode, ajoutez la méthode à la classe de composant.

.. code-block::

    currentClasses: Record<string, boolean> = {};
  /* . . . */
  setCurrentClasses() {
  // CSS classes: added/removed per current state of component properties
  this.currentClasses =  {
    saveable: this.canSave,
    modified: !this.isUnchanged,
    special:  this.isSpecial
  };
  }
..
Dans le modèle, ajoutez la ngClass liaison de propriété à currentClasses pour définir les classes de l'élément :
.. code-block::

    <div [ngClass]="currentClasses">This div is initially saveable, unchanged, and special.</div>
..

**Définir des styles en ligne avec NgStyle**
---------------------------------------------

.. code-block::

    currentStyles: Record<string, string> = {};
  /* . . . */
  setCurrentStyles() {
  // CSS styles: set per current state of component properties
  this.currentStyles = {
    'font-style':  this.canSave      ? 'italic' : 'normal',
    'font-weight': !this.isUnchanged ? 'bold'   : 'normal',
    'font-size':   this.isSpecial    ? '24px'   : '12px'
  };
  }
..
Pour définir les styles de l'élément, ajoutez une ngStyleliaison de propriété à currentStyles.  

.. code-block::

    <div [ngStyle]="currentStyles">
  This div is initially italic, normal weight, and extra large (24px).
  </div>
..

**Affichage et mise à jour des propriétés avec ngModel**
---------------------------------------------------------

Utilisez la NgModeldirective pour afficher une propriété de données et mettre à jour cette propriété lorsque 
l'utilisateur apporte des modifications.

Importez FormsModule -le et ajoutez-le à la liste de NgModule imports.

.. code-block::

  import { FormsModule } from '@angular/forms'; // <--- JavaScript import from Angular
  /* . . . */
  @NgModule({
  /* . . . */

  imports: [
    BrowserModule,
    FormsModule // <--- import into the NgModule
  ],
  /* . . . */
  })
  export class AppModule { }  
..
joutez une liaison sur un élément HTML et définissez-la égale à la propriété, ici .[(ngModel)]<form>name  

.. code-block::

    <label for="example-ngModel">[(ngModel)]:</label>
    <input [(ngModel)]="currentItem.name" id="example-ngModel">
..

**Directives structurelles intégrées**
_____________________________________

Cette section présente les directives structurelles intégrées les plus courantes :

- NgIf: crée ou supprime de manière conditionnelle des sous-vues à partir du modèle.
- NgFor—répétez un nœud pour chaque élément d'une liste.
- NgSwitch—un ensemble de directives qui basculent entre des vues alternatives.
  
**Ajouter ou supprimer un élément avec NgIf**
---------------------------------------------

.. code-block::

    <app-item-detail *ngIf="isActive" [item]="item"></app-item-detail>
..    

Lorsque l' isActiveexpression renvoie une valeur véridique, NgIfajoute le ItemDetailComponentau DOM. 
Lorsque l'expression est fausse, NgIfsupprime le ItemDetailComponentdu DOM et supprime le composant 
et tous ses sous-composants.

**Liste des articles avec NgFor**
----------------------------------

Utilisez la NgFordirective pour présenter une liste d'éléments.
.. code-block::

    <div *ngFor="let item of items">{{item.name}}</div>
..

Répétition d'une vue de composant
----------------------------------

Pour répéter un élément de composant, appliquez -le au sélecteur. 
Dans l'exemple suivant, le sélecteur est .*ngFor<app-item-detail>

.. code-block::

    <app-item-detail *ngFor="let item of items" [item]="item"></app-item-detail>
..

Suivi des articles avec *ngFor trackBy
--------------------------------------

Ajoutez une méthode au composant qui renvoie la valeur NgForà suivre. Dans cet exemple, la valeur à suivre est celle de 
l'élément id. Si le navigateur a déjà rendu id, Angular en garde la trace et ne réinterroge pas le serveur pour le même id.
.. code-block::

    trackByItems(index: number, item: Item): number { return item.id; }
..
Dans l'expression abrégée, définissez trackByla trackByItems()méthode.
.. code-block::

    <div *ngFor="let item of items; trackBy: trackByItems">
  ({{item.id}}) {{item.name}}
</div>

Changer de boîtier avec NgSwitch
---------------------------------
NgSwitch est un ensemble de trois directives :

- NgSwitch—une directive d'attribut qui modifie le comportement de ses directives associées.
- NgSwitchCase—directive structurelle qui ajoute son élément au DOM lorsque sa valeur liée est égale à la valeur de commutation et supprime sa valeur liée lorsqu'elle n'est pas égale à la valeur de commutation.
- NgSwitchDefault—directive structurelle qui ajoute son élément au DOM lorsqu'il n'y a pas de NgSwitchCase.

.. code-block::

   <div [ngSwitch]="currentItem.feature">
  <app-stout-item    *ngSwitchCase="'stout'"    [item]="currentItem"></app-stout-item>
  <app-device-item   *ngSwitchCase="'slim'"     [item]="currentItem"></app-device-item>
  <app-lost-item     *ngSwitchCase="'vintage'"  [item]="currentItem"></app-lost-item>
  <app-best-item     *ngSwitchCase="'bright'"   [item]="currentItem"></app-best-item>
  <!-- . . . -->
  <app-unknown-item  *ngSwitchDefault           [item]="currentItem"></app-unknown-item>
  </div>
.. 
Dans le composant parent, définissez currentItem, pour l'utiliser dans l' expression.[ngSwitch]
.. code-block::

    currentItem!: Item;
..
Dans chaque composant enfant, ajoutez une item propriété d'entrée qui est liée au currentItemcomposant parent. 
Les deux extraits de code suivants montrent le composant parent et l'un des composants enfants. 
Les autres composants enfants sont identiques à StoutItemComponent.
.. code-block::

   export class StoutItemComponent {
  @Input() item!: Item;
  } 
..
Les directives Switch fonctionnent également avec les éléments HTML intégrés et les composants Web. Par exemple, 
vous pouvez remplacer le boîtier du <app-best-item>commutateur par un <div>comme suit.
.. code-block::

    <div *ngSwitchCase="'bright'"> Are you as bright as {{currentItem.name}}?</div>
..


**Injection de dépendances dans Angular**
_________________________________________


Les dépendances sont des services ou des objets dont une classe a besoin pour remplir sa fonction. 
L'injection de dépendances, ou DI, est un modèle de conception dans lequel une classe demande des 
dépendances à des sources externes plutôt que de les créer.

Création d'un service injectable
--------------------------------
Pour générer une nouvelle HeroServiceclasse dans le src/app/heroesdossier
.. code-block::

ng generate service heroes/hero
..
Cette commande crée la valeur par défaut suivante HeroService.
.. code-block::
    import { Injectable } from '@angular/core';

 @Injectable({
  providedIn: 'root',
 })
 export class HeroService {
  constructor() { }
 }
..
Ensuite, pour obtenir les données fictives du héros, ajoutez une getHeroes()méthode qui renvoie les héros de mock.heroes.ts.
.. code-block::
    import { Injectable } from '@angular/core';
    import { HEROES } from './mock-heroes';

    @Injectable({
  // declares that this service should be created
  // by the root application injector.
  providedIn: 'root',
   })
   export class HeroService {
  getHeroes() { return HEROES; }
   }
..

Services d'injection
--------------------
Pour injecter une dépendance dans un composant constructor(), fournissez un argument constructeur avec le type de dépendance. 
L'exemple suivant spécifie le HeroServicedans le HeroListComponentconstructeur. Le type de heroServiceest HeroService.
.. code-block::
    constructor(heroService: HeroService)
..
Utiliser des services dans d'autres services
--------------------------------------------
Lorsqu'un service dépend d'un autre service, suivez le même schéma que l'injection dans un composant. 
Dans l'exemple suivant HeroServicedépend d'un Loggerservice pour rapporter ses activités.
.. code-block::
    import { Injectable } from '@angular/core';
 import { HEROES } from './mock-heroes';
 import { Logger } from '../logger.service';

 @Injectable({
  providedIn: 'root',
 })
 export class HeroService {

  constructor(private logger: Logger) {  }

  getHeroes() {
    this.logger.log('Getting heroes ...');
    return HEROES;
  }
 }
..
