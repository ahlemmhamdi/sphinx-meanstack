
.. _introduction:

====================================================================
programmation fonctionnelle: Définition - Histoire - Exemple
====================================================================

**Définition**
______________

La programmation fonctionnelle (également appelée FP) est une façon 
de penser la construction logicielle en créant des fonctions pures. 
Il évite les concepts d'état partagé, les données mutables,
Il ne repose pas sur des données en dehors de la fonction actuelle
et ne modifie pas les données qui existent en dehors de la fonction actuelle.


**Histoire**
______________

* La base de la programmation fonctionnelle est le Lambda Calculus. Il a été développé dans les années 1930 pour l'application fonctionnelle, la définition et la récursivité
* LISP a été le premier langage de programmation fonctionnel. McCarthy l'a conçu en 1960
* À la fin des années 70, des chercheurs de l'Université d'Édimbourg ont défini le ML (Meta Language)
* Au début des années 80, le langage Hope ajoute des types de données algébriques pour la récursivité et le raisonnement équationnel
* En 2004 Innovation du langage fonctionnel 'Scala.'

Exemple
----------
- Ceci est une fonction non fonctionnelle:

.. code-block::

 a = 0
 def increment1():
 global a
 a += 1
..

- Ceci est une fonction fonctionnelle:

.. code-block::

 def increment2(a):
 return a + 1
..

