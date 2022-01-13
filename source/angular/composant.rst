.. _composant:

========================
Angular: composant
========================



**Composant**
_____________


Création d'un composant à l'aide de la CLI angulaire
----------------------------------------------------

1. Depuis une fenêtre de terminal, accédez au répertoire contenant votre application.
2. Exécutez la ng generate component <component-name>commande, où <component-name>est le nom de votre nouveau composant.

Créer un composant manuellement
-------------------------------

1. Accédez à votre répertoire de projet Angular.

2. Créez un nouveau fichier, <component-name>.component.ts.

3. En haut du fichier, ajoutez l'instruction import suivante.
   
.. code-block::

    import { Component } from '@angular/core';
..

4. ajoutez un décorateur.@Component

.. code-block::

   @Component({
   })
..
5. Choisissez un sélecteur CSS pour le composant.

.. code-block::

   @Component({
  selector: 'app-component-overview',
  })
..
6. Définissez le modèle HTML que le composant utilise pour afficher les informations.
   
.. code-block::

    @Component({
  selector: 'app-component-overview',
  templateUrl: './component-overview.component.html',
   })
..
7. Sélectionnez les styles pour le modèle du composant. 
   
.. code-block::

    @Component({
  selector: 'app-component-overview',
  templateUrl: './component-overview.component.html',
  styleUrls: ['./component-overview.component.css']
  })
..

8. Ajoutez une classinstruction qui inclut le code du composant.
.. code-block::

  export class ComponentOverviewComponent {

  }
..