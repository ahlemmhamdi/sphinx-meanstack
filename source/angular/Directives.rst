.. _directives:

========================
Angular: directives
========================



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
Utilisation NgClassavec une méthode
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
Dans le modèle, ajoutez la ngClassliaison de propriété à currentClassespour définir les classes de l'élément :
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
