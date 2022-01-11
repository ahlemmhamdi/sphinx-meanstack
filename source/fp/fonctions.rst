

.. _fonctions:

========================================================================
programmation fonctionnelle: Introduction - Exemple - Fonctions_mathematiques 
========================================================================

**Introduction**
________________

La programmation fonctionnelle est un style de programmation dont les concepts fondamentaux sont
les notions de valeur, de fonction et d'application d'une fonction à un valeur.
Le terme fonction est à prendre ici au sens mathématique du terme, c'est-à-dire une relation entre
deux ensembles A et B telle que tout élément de l'ensemble A soit en relation avec au plus un élément de
l'ensemble B. Si on nomme f cette fonction, et x un élément de A on note habituellement f(x) l'élement
de B associé à x et on dit que f(x) est l'image de x par f si cette image est définie.


**Exemple**
___________

Voici quelques exemples de fonctions


1. une fonction numérique

                f : R → R

                x → f(x) =
                √x2+1/x-1


Les ensembles A et B sont ici tous deux égaux à l'ensemble R des nombres réels.
 Tout réel x != 1 a une image par f.


2. la fonction qui à un mot sur un alphabet A associe sa longueur


                length : A* → N

                u → |u|

L'ensemble A est l'ensemble A* des mots sur l'alphabet A, et l'ensemble B est l'ensemble N des
entiers naturels. Tout mot a une image par cette fonction.


3. la fonction qui à deux entiers associe leur somme


                add : Z x Z → Z

                (n1, n2) → n1 + n2


**Fonctions_mathematiques**
___________________________

• Def : une fonction mathématique est un mappage des membres d'un ensemble, appelé l'ensemble de domaine, à un autre ensemble, appelé l'ensemble de plage.
• Le lambda calcul est un système mathématique formel conçu par Alonzo Church pour étudier les fonctions, l'application des fonctions et la récursivité.
• Une expression lambda spécifie le(s) paramètre(s) et le mappage d'une fonction sous la forme suivante

          ? ?x . x * x * x

  for the function cube (x) = x * x * x

• Lambda expressions describe nameless functions
• Lambda expressions are applied to parameter(s) by placing the parameter(s) after the expression

          ( ? ? x . x * x * x) 3 => 3*3*3 => 27

          ( ? ? x,y . (x-y)*(y-x)) (3,5) => (3-5)*(5-3) => -4