.. _configuration:

=====================================================================================
Angular:  Installer la CLI angulaire 
=====================================================================================

Conditions préalables
----------------------

Pour installer Angular sur votre système local, vous avez besoin des éléments suivants :

- Node.js
Pour plus d'informations sur l'installation de Node.js, consultez https://nodejs.org/en/download/ ,Si vous ne savez pas 
quelle version de Node.js s'exécute sur votre système, exécutez-la node -v dans une fenêtre de terminal.
- gestionnaire de paquets npm
Les applications Angular, Angular CLI et Angular dépendent de paquets npm pour de nombreuses fonctionnalités et fonctions. 
Pour télécharger et installer des packages npm, vous avez besoin d'un gestionnaire de packages npm.
Pour vérifier que le client npm est installé, exécutez-le npm -vdans une fenêtre de terminal.

**Installer la CLI angulaire**
______________________________

ouvrez une fenêtre de terminal et exécutez la commande suivante :

.. code-block::

    npm install -g @angular/cli
..

Créer un espace de travail et une première application
-------------------------------------------------------

.. code-block::

    ng new my-app
..

Exécuter l'application
-----------------------

1. Accédez au dossier de l'espace de travail, tel que my-app.
2. Exécutez la commande suivante :*
.. code-block::
  cd my-app
  ng serve --open
..
