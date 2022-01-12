.. _an-introduction:

=====================================================================================
Angular: Qu'est-ce qu'Angular  - pourquoi Angular - Les concepts d'Angular
=====================================================================================

**Qu'est-ce qu'Angular**
__________________________

Angular est une plateforme de développement, construite sur TypeScript
En tant que plate-forme, Angular comprend :

- Un framework basé sur des composants pour créer des applications Web évolutives
  
- Une collection de bibliothèques bien intégrées qui couvrent une grande variété de fonctionnalités, notamment le routage, la gestion des formulaires, la communication client-serveur, etc.

- Une suite d'outils de développement pour vous aider à développer, créer, tester et mettre à jour votre code

**pourquoi Angular**
_____________________

Angular est une plate-forme et un framework permettant de créer des applications clientes 
d'une seule page à l'aide de HTML et de TypeScript. Angular est écrit en TypeScript. 
Il implémente les fonctionnalités principales et facultatives sous la forme d'un ensemble 
de bibliothèques TypeScript que vous importez dans vos applications.

**historique**
_______________

- 2010:AngularJS généralement appelé « Angular.js » ou Angular 1.x
- 2016:Angular 2 est une réécriture complète de la même équipe qui a construit AngularJS.
- Angular 3 a été ignoré.
- Mars 2017:Angular 4 L'équipe Angular a mis l'accent sur la création d'applications angulaires plus rapides et compactes.
- Novembre 2017:Angular 5  une ventilation de certains des changements les plus importants de la v5. 
- Mai 2018:Angular 6 Il a été publié avec Angular CLI 6 et Material 6.
- Octobre 2018:Angular 7 Il est publié avec des améliorations de performances et des fonctionnalités intéressantes 
telles que les invites CLI, le défilement virtuel et le glisser-déposer.
- Mai 2019:Angular 8 publié synchronisé avec Angular CLI 8 et Angular Material 8.
- Février 2020: Angular 9 est venu avec le compilateur Ivy le plus attendu .
- Juin 2020:Angular 10 Il s'agit de la version majeure synchronisée avec Angular CLI 10 et Angular Material 10.
- Novembre 2020: Angular 11 Cette version est publiée avec quelques corrections de bogues populaires et quelques bonnes fonctionnalités.
- Mai 2021:Angular 12 est publiée avec des fonctionnalités intéressantes, la meilleure est la prise en charge de Tailwind CSS.
- Novembre 2021:Angular 13 a continué d'avancer avec Ivy. 


**Les concepts d'Angular**
___________________________

L'architecture d'une application Angular repose sur certains concepts fondamentaux. Les blocs de construction 
de base du framework Angular sont des composants angulaires organisés en NgModules . 
NgModules collecte le code associé dans des ensembles fonctionnels ; une application Angular est définie par 
un ensemble de NgModules. Une application a toujours au moins un module racine qui permet l'amorçage 
et a généralement beaucoup plus de modules de fonctionnalités .

- Les composants définissent des vues , qui sont des ensembles d'éléments d'écran parmi lesquels Angular peut choisir et modifier en fonction de la logique et des données de votre programme.

- Les composants utilisent des services , qui fournissent des fonctionnalités spécifiques non directementliées aux vues. Les fournisseurs de services peuvent être injectés dans les composants en tant que dépendances ,ce qui rend votre code modulaire, réutilisable et efficace.

Les modules, composants et services sont des classes qui utilisent des décorateurs . Ces décorateurs marquent leur type 
et fournissent des métadonnées qui indiquent à Angular comment les utiliser.

- Les métadonnées d'une classe de composant l'associent à un modèle qui définit une vue. Un modèle combine du HTML ordinaire avec des directives Angular et un balisage de liaison qui permettent à Angular de modifier le HTML avant de le rendre pour affichage.
 
- Les métadonnées d'une classe de service fournissent les informations dont Angular a besoin pour les rendre disponibles aux composants via l' injection de dépendances (DI) .

Les composants d'une application définissent généralement de nombreuses vues, organisées hiérarchiquement. Angular fournit 
le Routerservice pour vous aider à définir des chemins de navigation parmi les vues. Le routeur offre des capacités de 
navigation sophistiquées dans le navigateur.

Modules
--------

Les NgModules angulaires diffèrent et complètent les modules JavaScript (ES2015). Un NgModule déclare un contexte de 
compilation pour un ensemble de composants dédié à un domaine d'application, un flux de travail ou un ensemble de 
capacités étroitement lié. Un NgModule peut associer ses composants à du code associé, tel que des services, pour 
former des unités fonctionnelles.

Chaque application Angular a un module racine , nommé par convention AppModule, qui fournit le mécanisme d'amorçage qui
lance l'application. Une application contient généralement de nombreux modules fonctionnels.

Comme les modules JavaScript, NgModules peut importer des fonctionnalités d'autres NgModules et permettre à leurs propres
fonctionnalités d'être exportées et utilisées par d'autres NgModules. Par exemple, pour utiliser le service de routeur 
dans votre application, vous importez le RouterNgModule.

L'organisation de votre code en modules fonctionnels distincts aide à gérer le développement d'applications complexes et 
à concevoir pour la réutilisabilité. De plus, cette technique vous permet de profiter du lazy-loading, c'est -à- dire du 
chargement de modules à la demande, pour minimiser la quantité de code à charger au démarrage.

Composants
----------

Chaque application Angular a au moins un composant, le composant racine qui connecte une hiérarchie de composants avec le 
modèle d'objet de document de page (DOM). Chaque composant définit une classe qui contient des données d'application et 
une logique, et est associé à un modèle HTML qui définit une vue à afficher dans un environnement cible.

Le décorateur identifie la classe immédiatement en dessous en tant que composant et fournit le modèle et les métadonnées 
spécifiques au composant associées.@Component()

Modèles, directives et liaison de données
-----------------------------------------

Un modèle combine du HTML avec un balisage angulaire qui peut modifier les éléments HTML avant qu'ils ne soient affichés. 
Les directives de modèle fournissent la logique du programme et le balisage de liaison connecte vos données d'application 
et le DOM. Il existe deux types de liaison de données :

- La liaison d'événement permet à votre application de répondre aux entrées de l'utilisateur dans l'environnement cible en 
mettant à jour vos données d'application.
- La liaison de propriété vous permet d'interpoler les valeurs calculées à partir des données de votre application dans le 
code HTML.

Avant qu'une vue ne soit affichée, Angular évalue les directives et résout la syntaxe de liaison dans le modèle pour 
modifier les éléments HTML et le DOM, en fonction des données et de la logique de votre programme. Angular prend en charge 
la liaison de données bidirectionnelle , ce qui signifie que les modifications du DOM, telles que les choix de l'utilisateur, 
sont également reflétées dans les données de votre programme.

Vos modèles peuvent utiliser des canaux pour améliorer l'expérience utilisateur en transformant les valeurs pour l'affichage. 
Par exemple, utilisez des barres verticales pour afficher les dates et les valeurs monétaires adaptées aux paramètres 
régionaux d'un utilisateur. Angular fournit des tuyaux prédéfinis pour les transformations courantes, et vous pouvez 
également définir vos propres tuyaux.

Services et injection de dépendances
------------------------------------

Pour les données ou la logique qui ne sont pas associées à une vue spécifique et que vous souhaitez partager entre les 
composants, vous créez une classe de service . Une définition de classe de service est immédiatement précédée du décorateur. 
Le décorateur fournit les métadonnées qui permettent à d'autres fournisseurs d'être injectés en tant que dépendances dans 
votre classe.@Injectable()

L'injection de dépendances (DI) vous permet de garder vos classes de composants simples et efficaces. Ils ne récupèrent pas 
les données du serveur, ne valident pas les entrées de l'utilisateur ou ne se connectent pas directement à la console ; 
ils délèguent ces tâches à des services.

Routage
-------
Angular RouterNgModule fournit un service qui vous permet de définir un chemin de navigation parmi les différents états de 
l'application et d'afficher les hiérarchies dans votre application. Il est modelé sur les conventions de navigation 
familières du navigateur :

- Entrez une URL dans la barre d'adresse et le navigateur accède à une page correspondante.

- Cliquez sur les liens sur la page et le navigateur accède à une nouvelle page.

- Cliquez sur les boutons Précédent et Suivant du navigateur et le navigateur navigue dans l'historique des pages que vous 
avez consultées.

Le routeur mappe les chemins de type URL aux vues plutôt qu'aux pages. Lorsqu'un utilisateur effectue une action, 
telle qu'un clic sur un lien, qui chargerait une nouvelle page dans le navigateur, le routeur intercepte le comportement du 
navigateur et affiche ou masque les hiérarchies de vues.

Si le routeur détermine que l'état actuel de l'application nécessite une fonctionnalité particulière et que le module qui 
le définit n'a pas été chargé, le routeur peut charger paresseux le module à la demande.

Le routeur interprète une URL de lien en fonction des règles de navigation dans la vue et de l'état des données de votre 
application. Vous pouvez accéder à de nouvelles vues lorsque l'utilisateur clique sur un bouton ou sélectionne dans une 
liste déroulante, ou en réponse à un autre stimulus provenant de n'importe quelle source. Le routeur enregistre l'activité 
dans l'historique du navigateur, de sorte que les boutons Précédent et Suivant fonctionnent également.

Pour définir des règles de navigation, vous associez des chemins de navigation à vos composants. Un chemin utilise une 
syntaxe de type URL qui intègre vos données de programme, de la même manière que la syntaxe de modèle intègre vos vues 
avec vos données de programme. Vous pouvez ensuite appliquer la logique du programme pour choisir les vues à afficher 
ou à masquer, en réponse à la saisie de l'utilisateur et à vos propres règles d'accès.


