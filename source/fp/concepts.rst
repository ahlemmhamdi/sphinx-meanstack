.. _concepts:

======================================================
programmation fonctionnelle:  Quelques concepts de PF 
======================================================

**Quelques concepts de PF**
___________________________


• Un certain nombre de concepts de langage de programmation intéressants sont apparus, notamment :

- Fonctions au curry
- Inférence de type
- Polymorphisme
- Fonctions d'ordre supérieur
- Abstraction fonctionnelle
- Évaluation paresseuse


Fonctions au curry
-------------------


• Le logicien Frege notait en 1883 que nous n'avons besoin que des fonctions d'un argument.

- On peut remplacer une fonction f(x,y) par une nouvelle fonction f'(x) qui lorsqu'elle est appelée
produit une fonction d'un autre argument pour calculer f(x,Y).
- Soit : (f'(x))(y) = f (x,y)

• Haskell Curry a développé une logique combinatoire qui a utilisé cette idée.

• On appelle f' une forme « curry » de la fonction f.

• Deux opérations :

- Au curry : ((a,b) -> c) -> (a -> b -> c)
- Pour uncurry : (a -> b -> c) -> ((a,b) -> c)

Inférence de type
------------------

• Def : capacité du langage à déduire des types sans que le programmeur fournisse des signatures de type.

• SML ex : fun min(a:real,b) = if a > b then b else a

- le type de a doit être donné, mais cela suffit alors pour déterminer le type de b et le type de min
- Que faire si le type de a n'est pas spécifié ? Il peut s'agir d'entiers ou de booléens ou…

• Haskell (comme avec ML) garantit la sécurité des types (s'il compile, alors c'est la sécurité des types)

- Haskell ex : eq = (a = b)
- une fonction polymorphe qui a un type de retour bool, suppose seulement que ses deux arguments sont du même type et peut se voir appliquer l'opérateur d'égalité.

• L'utilisation excessive de l'inférence de type dans les deux langues est déconseillée

- les déclarations sont une aide à la conception
- les déclarations sont une aide à la documentation
- les déclarations sont une aide au débogage

Polymorphisme
-------------

• ML:
fun factorial (0) = 1
= | factorial (n) = n * factorial (n - 1);

-ML en déduit que factorielle est une fonction entière : int -> int

• Haskell:

factorial (0) = 1
factorial (n) = n * factorial (n - 1)

-Haskell en déduit que factorielle est une fonction (numérique) :
Num a => a -> a


Fonctions d'ordre supérieur
---------------------------

• Définitions :

- fonctions d'ordre zéro : données au sens traditionnel.
- fonctions du premier ordre : fonctions qui opèrent sur des fonctions d'ordre zéro.
- fonctions de second ordre : fonctionnent au premier ordre

• En général, les fonctions d'ordre supérieur (HOF) sont celles qui peuvent opérer sur des fonctions de n'importe quel ordre tant que les types correspondent.

- Les HOF sont généralement polymorphes

• Les fonctions d'ordre supérieur peuvent prendre d'autres fonctions comme arguments et produire des fonctions comme valeurs.

- La programmation applicative a souvent été considérée comme l'application de fonctions de premier ordre.
- La programmation fonctionnelle a été considérée comme incluant des fonctions d'ordre supérieur : les fonctionnelles.


Abstraction fonctionnelle
--------------------------

• La programmation fonctionnelle permet une abstraction fonctionnelle
 qui n'est pas prise en charge dans les langages impératifs,
 à savoir la définition et l'utilisation de fonctions qui prennent
 des fonctions comme arguments et renvoient des fonctions comme valeurs.

- prend en charge le raisonnement de niveau supérieur
- simplifie les preuves de correction
• Exemples simples :

Mapper et filtrer dans Scheme

- (map square (1 2 3 4)) => (1 4 9 16)
- (filter prime (between 1 15)) => (1 2 3 5 7 11 13)

• (define (map f l)

; Map applies a function f to elements of list l returning list of the results.
(if (null? l) nil (cons (f (first l)) (map f (rest l)))))

• (define filter (f l)

; (filter f l)returns a list of those elements of l for which f is true
(if (null? L )
nil
(if (f (first l)) (cons (first l) (filter f (cdr l))) (filter f (cdr l)))))))



Évaluation paresseuse
----------------------

• Une stratégie d'évaluation dans laquelle les arguments d'une fonction sont évalués uniquement lorsque cela est nécessaire pour le calcul.

• Pris en charge par de nombreux FPL, notamment Scheme, Haskell et Common Lisp.

• Très utile pour traiter des flux de données très volumineux ou infinis.

• Généralement implémenté à l'aide de fermetures - des structures de données contenant toutes les informations requises pour évaluer l'expression.

• Son contraire, l'évaluation avide, est la valeur par défaut habituelle dans un langage de programmation dans lequel les arguments d'une fonction sont toujours évalués avant que la fonction ne soit appliquée.