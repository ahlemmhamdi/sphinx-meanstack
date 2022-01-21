.. _methodes:

=====================================================================================
Express: Methods 
=====================================================================================

**Méthodes**
_____________

express.json([options])
-----------------------
Il s'agit d'une fonction middleware intégrée dans Express. Il analyse les requêtes entrantes avec des charges utiles JSON 
et est basé sur body-parser .

Renvoie un middleware qui analyse uniquement JSON et ne regarde que les requêtes où l' en- Content-Typetête correspond à 
l' typeoption. Cet analyseur accepte tout encodage Unicode du corps et prend en charge l'inflation automatique des gzipet 
des deflateencodages.

Un nouvel bodyobjet contenant les données analysées est rempli sur l' requestobjet après le middleware (c'est-à-dire req.body), 
ou un objet vide ( {}) s'il n'y avait pas de corps à analyser, si le Content-Typen'était pas mis en correspondance ou si une erreur s'est produite.

Le tableau suivant décrit les propriétés de l' optionsobjet facultatif.

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Type          |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Active ou désactive la gestion des corps dégonflés   | booléen      |  true                 |
|      inflate        |(compressés) ; lorsqu'il est désactivé, les corps    |              |                       |
|                     |dégonflés sont rejetés.                              |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       limit         |Contrôle la taille maximale du corps de la requête.  |              |                       |
|                     |S'il s'agit d'un nombre, la valeur spécifie le nombre| Mixte        |    "100kb"            |          
|                     |d'octets ; s'il s'agit d'une chaîne, la valeur est   |              |                       |
|                     | transmise à la bibliothèque d' octets pour analyse. |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       reviver       |L' reviveroption est passée directement à JSON.      |              |                       |
|                     |parse comme second argument. Vous pouvez trouver plus| Une fonction |    null               |          
|                     |d'informations sur cet argument dans la documentation|              |                       |
|                     | MDN sur JSON.parse .                                |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       strict        |Active ou désactive uniquement l'acceptation de      |              |                       |
|                     |tableaux et d'objets ; lorsqu'il est désactivé       | booléen      |    true               |          
|                     |acceptera tout ce qui JSON.parseaccepte.             |              |                       |
|                     | MDN sur JSON.parse .                                |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       type          |Ceci est utilisé pour déterminer quel type de média  |              |                       |
|                     |le middleware analysera. Cette option peut être une  | Mixte        |    "application/json" |          
|                     |chaîne, un tableau de chaînes ou une fonction.       |              |                       |
|                     |S'il ne s'agit pas d'une fonction, l' typeoption est |              |                       |
|                     |transmise directement à la bibliothèque type-is      |              |                       |
|                     |et cela peut être un nom d'extension (comme json),   |              |                       |
|                     |un type mime (comme application/json) , un type mime |              |                       |
|                     |(comme application/json) ou un type mime avec        |              |                       |
|                     |un caractère générique (comme */*ou */json). S'il    |              |                       |
|                     |s'agit d'une fonction, l' typeoption est appelée en  |              |                       |
|                     |tant que fn(req)et la requête est analysée si elle   |              |                       |
|                     |renvoie une valeur véridique.                        |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       verify        |Cette option, si elle est fournie, est appelée verify|              |                       |
|                     |(req, res, buf, encoding), où buf est un Buffer du   | Une fonction |    undefined          |          
|                     |corps brut de la requête et encodingest l'encodage   |              |                       |
|                     |de la requête. L'analyse peut être interrompue en    |              |                       |
|                     |en lançant une erreur.                               |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+

express.raw([options])
-----------------------

Il s'agit d'une fonction middleware intégrée dans Express. Il analyse les charges utiles des requêtes entrantes dans un 
Bufferet est basé sur body-parser .

Renvoie un middleware qui analyse tous les corps en tant que Bufferet ne regarde que les requêtes où l'en- Content-Typetête 
correspond à l' typeoption. Cet analyseur accepte tout encodage Unicode du corps et prend en charge l'inflation automatique 
des gzipet des deflateencodages.

Un new body Buffercontenant les données analysées est rempli sur l' requestobjet après le middleware (c'est-à-dire req.body)
, ou un objet vide ( {}) s'il n'y avait pas de corps à analyser, si le Content-Typen'était pas mis en correspondance ou si 
une erreur s'est produite.

Le tableau suivant décrit les propriétés de l' options objet facultatif.

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Type          |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Active ou désactive la gestion des corps dégonflés   | booléen      |  true                 |
|      inflate        |(compressés) ; lorsqu'il est désactivé, les corps    |              |                       |
|                     |dégonflés sont rejetés.                              |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       limit         |Contrôle la taille maximale du corps de la requête.  |              |                       |
|                     |S'il s'agit d'un nombre, la valeur spécifie le nombre| Mixte        |    "100kb"            |          
|                     |d'octets ; s'il s'agit d'une chaîne, la valeur est   |              |                       |
|                     | transmise à la bibliothèque d' octets pour analyse. |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       type          |Ceci est utilisé pour déterminer quel type de média  |              |                       |
|                     |le middleware analysera. Cette option peut être une  | Mixte        |"application/octet     |          
|                     |chaîne, un tableau de chaînes ou une fonction.       |              | -stream"              |
|                     |S'il ne s'agit pas d'une fonction, l' typeoption est |              |                       |
|                     |transmise directement à la bibliothèque type-is      |              |                       |
|                     |et cela peut être un nom d'extension (comme json),   |              |                       |
|                     |un type mime (comme application/json) , un type mime |              |                       |
|                     |(comme application/json) ou un type mime avec        |              |                       |
|                     |un caractère générique (comme */*ou */json). S'il    |              |                       |
|                     |s'agit d'une fonction, l' typeoption est appelée en  |              |                       |
|                     |tant que fn(req)et la requête est analysée si elle   |              |                       |
|                     |renvoie une valeur véridique.                        |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       verify        |Cette option, si elle est fournie, est appelée verify|              |                       |
|                     |(req, res, buf, encoding), où buf est un Buffer du   | Une fonction |    undefined          |          
|                     |corps brut de la requête et encodingest l'encodage   |              |                       |
|                     |de la requête. L'analyse peut être interrompue en    |              |                       |
|                     |en lançant une erreur.                               |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+

express.Router([options])
-------------------------

Crée un nouvel objet routeur .
.. code-block:: 

    var routeur = express . Routeur ( [ options ] )
..
optionsLe paramètre facultatif spécifie le comportement du routeur.

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Disponibilité |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Activez la sensibilité à la casse.                   |              |Désactivé par défaut,  |
|    caseSensitive    |                                                     |              |traitant "/Foo" et     |
|                     |                                                     |              |"/foo" comme identiques|
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|    mergeParams      |Conservez les req.paramsvaleurs du routeur parent.   |              |                       |
|                     |Si le parent et l'enfant ont des noms de paramètres  | 4.5.0+       |    false              |          
|                     |en conflit, la valeur de l'enfant est prioritaire.   |              |                       |
|                     |                                                     |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|      strict         |Activez le routage strict.                           |              |Désactivé par défaut,  |
|                     |                                                     |              |"/foo" et "/foo/" sont |          
|                     |                                                     |              |traités de la même     |
|                     |                                                     |              |manière par le routeur.|
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+

express.static(racine, [options])
---------------------------------

L' rootargument spécifie le répertoire racine à partir duquel servir les actifs statiques. La fonction détermine le fichier 
à servir en le combinant req.urlavec le rootrépertoire fourni. Lorsqu'un fichier n'est pas trouvé, au lieu d'envoyer 
une réponse 404, il appelle next()à la place pour passer au middleware suivant, permettant l'empilement et les replis.

Le tableau suivant décrit les propriétés de l' optionsobjet. Voir aussi l' exemple ci-dessous .

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Type          |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Détermine comment les fichiers de points (fichiers   |Chaîne de     |"ignorer"              |
|   dotfiles          |ou répertoires commençant par un point ".")          |caractères    |                       |
|                     |sont traités.                                        |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Activer ou désactiver la génération d'etag           |booléen       |true                   |
|   etag              |REMARQUE : express.staticenvoie toujours des ETags   |              |                       |
|                     |faibles.                                             |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Définit les extensions de fichier de secours :       |Mixte         |false                  |
|   extensions        |si un fichier est introuvable, recherchez les        |              |                       |
|                     |fichiers avec les extensions spécifiées et servez le |              |                       |
|                     |premier trouvé. Exemple : ['html', 'htm'].	        |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Laissez les erreurs client passer sous forme de      |booléen       |true                   |
|   fallthrough       |requêtes non gérées, sinon transférez une erreur     |              |                       |
|                     |client.                                              |              |                       |
|                     |                                          	        |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Activez ou désactivez la immutabledirective dans     |booléen       |false                  |
|   immutable         |l'en- Cache-Controltête de réponse. Si elle est      |              |                       |
|                     |activée, l' maxAgeoption doit également être         |              |                       |
|                     |spécifiée pour activer la mise en cache. La immutable|              |                       |
|                     |directive empêchera les clients pris en charge       |              |                       |
|                     |de faire des demandes conditionnelles pendant la     |              |                       |
|                     |durée de vie de l' maxAgeoption pour vérifier si le  |              |                       |
|                     |fichier a changé.                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Envoie le fichier d'index de répertoire spécifié.    |Mixte         |"index.html"           |
|   index             |Définissez sur falsepour désactiver l'indexation des |              |                       |
|                     |répertoires.                                         |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Définissez l' Last-Modifieden-tête sur la date       |booléen       |true                   |
|   lastModified      |de la dernière modification du fichier sur le système|              |                       |
|                     |d'exploitation.                                      |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Définissez la propriété max-age de l'en-tête Cache-  |Nombre        |0                      |
|   maxAge            |Control en millisecondes ou une chaîne au  format ms |              |                       |
|                     |                                                     |              |                       |
|                     |                                          	        |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Rediriger vers "/" de fin lorsque le nom de chemin   |booléen       |true                   |
|   redirect          |est un répertoire.                                   |              |                       |
|                     |                                                     |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Fonction permettant de définir les en-têtes HTTP     |Une fonction  |                       |
|   setHeaders        |à servir avec le fichier.                            |              |                       |
|                     |                                                     |              |                       |
|                     |                                          	        |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+

Exemple de express.static
Voici un exemple d'utilisation de la express.staticfonction middleware avec un objet options élaboré :

.. code-block::

    var options =  { 
  dotfiles :  'ignore' , 
  etag :  false , 
  extensions :  [ 'htm' ,  'html' ] , 
  index :  false , 
  maxAge :  '1d' , 
  redirect :  false , 
  setHeaders :  function  ( res , path , stat )  { 
    rés . set ( 'x-horodatage' , Date . maintenant( ) ) 
  } 
  }

  application . use ( express . static ( 'public' , options ) )

..
express.text([options])
-----------------------

Il s'agit d'une fonction middleware intégrée dans Express. Il analyse les charges utiles des requêtes entrantes dans une 
chaîne et est basé sur body-parser .

Renvoie un middleware qui analyse tous les corps sous forme de chaîne et ne regarde que les requêtes dont 
l' en- Content-Typetête correspond à l' typeoption. Cet analyseur accepte tout encodage Unicode du corps et prend en charge 
l'inflation automatique des gzipet des deflateencodages.

Une nouvelle bodychaîne contenant les données analysées est renseignée sur l' requestobjet après le middleware (c'est-à-dire
req.body), ou un objet vide ( {}) s'il n'y avait pas de corps à analyser, si le Content-Typen'a pas été mis en correspondance
ou si une erreur s'est produite.

Le tableau suivant décrit les propriétés de l' optionsobjet facultatif.

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Type          |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Spécifiez le jeu de caractères par défaut pour le    |Chaîne de     |"utf-8"                |
|   defaultCharset    |contenu du texte si le jeu de caractères n'est pas   |caractères    |                       |
|                     |pécifié dans l'en- Content-Typetête de la demande.   |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Active ou désactive la gestion des corps dégonflés   | booléen      |  true                 |
|      inflate        |(compressés) ; lorsqu'il est désactivé, les corps    |              |                       |
|                     |dégonflés sont rejetés.                              |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       limit         |Contrôle la taille maximale du corps de la requête.  |              |                       |
|                     |S'il s'agit d'un nombre, la valeur spécifie le nombre| Mixte        |    "100kb"            |          
|                     |d'octets ; s'il s'agit d'une chaîne, la valeur est   |              |                       |
|                     | transmise à la bibliothèque d' octets pour analyse. |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       type          |Ceci est utilisé pour déterminer quel type de média  |              |                       |
|                     |le middleware analysera. Cette option peut être une  | Mixte        |"text/plain"           |          
|                     |chaîne, un tableau de chaînes ou une fonction.       |              |                       |
|                     |S'il ne s'agit pas d'une fonction, l' typeoption est |              |                       |
|                     |transmise directement à la bibliothèque type-is      |              |                       |
|                     |et cela peut être un nom d'extension (comme json),   |              |                       |
|                     |un type mime (comme application/json) , un type mime |              |                       |
|                     |(comme application/json) ou un type mime avec        |              |                       |
|                     |un caractère générique (comme */*ou */json). S'il    |              |                       |
|                     |s'agit d'une fonction, l' typeoption est appelée en  |              |                       |
|                     |tant que fn(req)et la requête est analysée si elle   |              |                       |
|                     |renvoie une valeur véridique.                        |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       verify        |Cette option, si elle est fournie, est appelée verify|              |                       |
|                     |(req, res, buf, encoding), où buf est un Buffer du   | Une fonction |    undefined          |          
|                     |corps brut de la requête et encodingest l'encodage   |              |                       |
|                     |de la requête. L'analyse peut être interrompue en    |              |                       |
|                     |en lançant une erreur.                               |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+

express.urlencodé([options])
----------------------------

Il s'agit d'une fonction middleware intégrée dans Express. Il analyse les requêtes entrantes avec des charges utiles codées 
en URL et est basé sur body-parser .

Renvoie un middleware qui analyse uniquement les corps codés en URL et ne regarde que les requêtes où l'en- Content-Typetête 
correspond à l' typeoption. Cet analyseur accepte uniquement l'encodage UTF-8 du corps et prend en charge l'inflation 
automatique des gzipet des deflateencodages.

Un nouvel bodyobjet contenant les données analysées est rempli sur l' requestobjet après le middleware (c'est-à-dire 
req.body), ou un objet vide ( {}) s'il n'y avait pas de corps à analyser, si le Content-Typen'était pas mis en 
correspondance ou si une erreur s'est produite. Cet objet contiendra des paires clé-valeur, où la valeur peut être 
une chaîne ou un tableau (quand extendedest false), ou n'importe quel type (quand extendedest true).

Le tableau suivant décrit les propriétés de l' optionsobjet facultatif.

+---------------------+-----------------------------------------------------+--------------+-----------------------+
|Propriété            | La description                                      |Type          |  Défaut               |
+=====================+=====================================================+==============+=======================+
|                     |Cette option permet de choisir entre analyser les    |booléen       |true                   |
|  extended           |données encodées en URL avec la querystring          |              |                       |
|                     |bibliothèque (quand false) ou la qsbibliothèque      |              |                       |
|                     |(quand true). La syntaxe « étendue » permetaux objets|              |                       |
|                     |riches et aux tableaux d'être encodés dans le format |              |                       |
|                     |encodé en URL, permettant une expérience de type JSON|              |                       |
|                     |avec encodage en URL. Pour plus d'informations,      |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|                     |Active ou désactive la gestion des corps dégonflés   | booléen      |  true                 |
|      inflate        |(compressés) ; lorsqu'il est désactivé, les corps    |              |                       |
|                     |dégonflés sont rejetés.                              |              |                       |
|                     |	                                                    |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       limit         |Contrôle la taille maximale du corps de la requête.  |              |                       |
|                     |S'il s'agit d'un nombre, la valeur spécifie le nombre| Mixte        |    "100kb"            |          
|                     |d'octets ; s'il s'agit d'une chaîne, la valeur est   |              |                       |
|                     | transmise à la bibliothèque d' octets pour analyse. |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|  parameterLimit     |Cette option contrôle le nombre maximal de paramètres|              |                       |
|                     |autorisés dans les données encodées en URL.          |    Nombre    |    1000               |          
|                     |Si une requête contient plus de paramètres que cette |              |                       |
|                     |valeur, une erreur sera levée.                       |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       type          |Ceci est utilisé pour déterminer quel type de média  |              |                       |
|                     |le middleware analysera. Cette option peut être une  | Mixte        |"application/x-        |          
|                     |chaîne, un tableau de chaînes ou une fonction.       |              | www-form-             |
|                     |S'il ne s'agit pas d'une fonction, l' typeoption est |              | urlencoded"           |
|                     |transmise directement à la bibliothèque type-is      |              |                       |
|                     |et cela peut être un nom d'extension (comme json),   |              |                       |
|                     |un type mime (comme application/json) , un type mime |              |                       |
|                     |(comme application/json) ou un type mime avec        |              |                       |
|                     |un caractère générique (comme */*ou */json). S'il    |              |                       |
|                     |s'agit d'une fonction, l' typeoption est appelée en  |              |                       |
|                     |tant que fn(req)et la requête est analysée si elle   |              |                       |
|                     |renvoie une valeur véridique.                        |              |                       |
|                     |                                                     |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
|       verify        |Cette option, si elle est fournie, est appelée verify|              |                       |
|                     |(req, res, buf, encoding), où buf est un Buffer du   | Une fonction |    undefined          |          
|                     |corps brut de la requête et encodingest l'encodage   |              |                       |
|                     |de la requête. L'analyse peut être interrompue en    |              |                       |
|                     |en lançant une erreur.                               |              |                       |
+---------------------+-----------------------------------------------------+--------------+-----------------------+
