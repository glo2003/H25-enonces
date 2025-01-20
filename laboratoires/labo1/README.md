# Laboratoire 1 - API Web

## Objectifs

- Apprendre les bases du Web et de HTTP/REST
- Utiliser Jersey pour contruire une API HTTP REST

## Partie 1 - Le Web

Le Web est une plateforme de communication et de distribution d'information. Sans aller trop en détail, c'est un réseau ou plusieurs **serveurs** (ordinateurs sur le Web) sont inter-connectés et identifiés par des adresses IP uniques (ex: `127.0.0.1`). De plus, d'autres ordinateurs peuvent se connecter dynamiquement au réseau afin d'intéragir avec les serveurs. Ces ordinateurs, comme le vôtre, sont appelés **client**. Eux-aussi possèdent une adresse IP, mais celle-ci change selon le réseau sur lequel il est connecté.

### Adresse et port

En plus de posséder une adresse IP en tant que client connecté à un réseau, votre ordinateur possède également un petit **réseau local**, c'est-à-dire dans lui-même. Ce réseau local possède également des adresses IP, mais celle-ci sont spéciales et réservées à ces réseaux internes. Pour vous connecter à votre propre ordinateur, il suffit d'utiliser l'adresse IP `0.0.0.0`, ou encore l'adresse du routeur `127.0.0.x`, où `x` dépend du routeur et du moment de connexion. Un alias à peu-près équivalent pour `0.0.0.0` est `localhost` (hôte local). Les "noms" de site Web (ou plutôt "domaines") tel que `google.com` sont simplement des alias qui pointent vers des adresses IP.

Chaque ordinateur possède également une liste de **ports**. Chaque port est comme une porte d'entrée vers un **processus** sur l'ordinateur. Chaque processus représente souvent un logiciel ou une technologie particulière. Par exemple, le port `80` est réservé aux communications HTTP. Chaque ordinateur possède également une liste de ports libre d'usage sur lesquel on peut démarrer n'importe quel processus, comme le serveur Web du projet. Les ports sont identifié par un `:` après l'adresse IP. Par exemple, `0.0.0.0:8080`.

### HTTP

HTTP est un protocole de communication Web. Il définit une structure d'information standard permettant à des ordinateurs de communiquer entre-eux. Un paquet HTTP provient d'abord d'une **requête** qui part du client vers le serveur, qui lui retourne au client une **réponse**.

Les requêtes sont entre-autres composées des parties suivantes :

1. Un **URL**, qui indique entre autre la destination que l'on souhaite atteindre
2. Une **méthode** (ou "verbe") qui indique le type d'action que l'on souhaite faire
3. Des **headers**, qui ajoutent des informations additionnelles
4. Un **body**, qui contient le message qu'on envoie

Les réponses sont entre-autres composées des parties suivantes :

1. Un **code de statut** (*status*), qui indique l'état de l'exécution. Par exemple: `200 Ok`, `301 Redirect` ou encore `404 Not Found`
2. Des headers, qui ajoutent des informations additionnelles
3. Un body, qui contient le message qu'on envoie

Nous verrons en pratique dans les laboratoires ce que représentent ces parties, comment les construires et comment les utiliser.

### URL

Un URL est composé de plusieurs parties :

1. Le **protocole** utilisé. Toujours suivie de `://`. Exemple: `http://` ou `https://`.
2. L'adresse du serveur (IP ou nom de domaine). Exemple: `google.com`.
3. Le numéro de port (par défaut: `80`). Toujours précédé de `:`. Exemple: `:8080`.
4. Le **path**, qui représente l'adresse interne du processus. On l'utilisera beaucoup avec Jersey pour définir des **routes**, c'est-à-dire des points d'accès dans notre application. Il peut être découpé en hiérachie séparée par des `/`. Exemple: `/restaurants/7637628131/reservations`.
5. Des **query parameters**, qui sont une forme d'information comme le body, mais envoyé directement dans l'URL. Commence toujours par un `?` et chaque paramètre est délimité par `&`. On indique ensuite le nom du paramètre, suivit d'un `=` et ensuite sa valeur (toujours interprété comme une `String`). On l'utilisera surtout pour des requêtes de type `GET`. Exemple: `?name=hello&page=2`.

En résumé, un URL complet pourrait ressembler à ceci : `http://localhost:8080/search/restaurants?name=alfredo`

### Méthode

Une méthode est comme un type de requête. Elle indique l'action que l'on désire effectuer. Ce n'est pas obligatoire de l'utiliser (toutes nos requêtes pourraient être des `GET`), mais ça aide à mieux définir et segmenter les paths. Ainsi, on pourrait avoir 2 méthodes pour un même path (ex: modifier vs. supprimer un restaurant), ce qui aboutirait vers 2 chemins différents dans l'application.

Parmi toutes les méthodes qui existent, voici celles qui sont intéressantes ainsi que leur utilisation populaire :

- `GET` : obtenir une ressource. Souvent utilisé avec des query parameters pour modifier les résultats (filtrer, trier, etc.)
- `POST` : envoyer une information. Souvent utilisé avec un body plutôt que des query parameters. Utile pour créer des ressources ou pour obtenir une information avec des filtres plus avancés.
- `PUT` ou `PATCH` : modifier une ressource complètement ou en partie, respectivement. Aussi souvent utilisé avec un body comme le `POST`.
- `DELETE` : supprimer une ressource. Souvent utilisé sans aucun body ni query param.

Lors de la description d'une fonctionalité de serveur Web, on va souvent identifier une **route** par la méthode suivi du path de l'URL, puisque c'est la combinaison des deux qui amène vers un chemin unique dans l'application. Par exemple, `POST /restaurants` ou `GET /restaurant/1234`.

### Body

Le body est une partie d'information libre décrite sous un format précis (*MIME type*). On peut y mettre du code binaire, du HTML, du texte, etc. Afin de spécifier le type de contenu, on doit envoyer un header nommé `Content-Type` avec lidentifiant du format envoyé. Parmi les formats existants, voici les plus populaires :

- `text/plain` pour du texte
- `text/html` pour du HTML (page Web)
- `application/json` pour du JSON
- `application/x-www-form-urlencoded` (je sais, pire nom) pour un ensemble de valeurs key/value encodé dans les query parameters de l'URL (quand on fait un `GET` mais pour envoyer de l'information)

Dans le cadre du TP, on utilisera le format JSON, puisqu'il est facile d'utilisation et extrêment populaire. Il se décrit sous la forme suivante :

```json
{ // Indique un objet. Ne pas oublier la portion fermante "}"
  "name": "Alfred", // Paires "key": value. Ici, la valeur est une 'string'.
  "age": 13, // Valeur de type 'number'
  "money": 123.45, // 'number' peut être un nombre à décimales
  "eligible": true, // un booléen
  "friends": [ // Une liste. Les éléments doivent être du même type.
    "Bob",
    "Roger"
  ],
  "phoneNumbers": [ // une liste...
    { // d'objets!
      "type": "work",
      "value": "1234567890"
    }
  ],
  "parent": null // les champs sont nullable. null == ne pas spécifier le champ.
}
```

De plus, la structure permise pour le body en JSON sera décrite à l'aide d'un **schéma** (noms des attributs, leur hiérarchie et leur type). Le format utilisé dans les TPs suivra de près la définition des type de Typescript (qui est la forme typée de Javascript), à l'exception des liste (décrites de façon plus claire). C'est une forme pratique puisqu'elle est pratiquement identique à la structure JSON, avec les guillements `"` en moins, et des points d'interrogation `?` pour les champs optionels. Par exemple, le body précédent peut être représenté par le schéma suivant :

```typescript
{
  name: string,
  age: number,
  money: number,
  friends: [string],
  phoneNumbers: [
    {
      type: string,
      value: string
    }
  ],
  parent?: string
}
```

### REST

REST est une convention permettant de structurer et d'uniformiser les routes que l'on définit pour notre application. La pratique de REST se base sur le fait que notre application gère des **ressources**. C'est un terme très large, mais pour faciliter les choses, on peut le voir comme un "objet" ou même comme une "classe". Par exemple, un "restaurant", un "employé", un "meuble" sont toutes des ressources. Dans l'URL, les ressources seront toujours affichées au pluriel.

Une fois que l'on a notre ressource, il est important de définir leur dépendances. Par exemple, un employé peut être indépendant, il peut également contenir un horaire ou encore faire partie d'une compagnie. Ces dépendances vont définir la hiérarchie des **path** dans notre URL.

Ensuite, on utilisera les méthodes HTTP décrites précédemment afin d'identifier les actions que l'ont désire effectuer sur nos ressources (`POST` pour créer, `GET` pour obtenir, `DELETE` pour supprimer, etc.)

Finalement, chaque ressource possède un identifiant unique (par type de ressource), qui permet de cibler une ressource précise.

Voici quelques exemples de routes basées sur la convention REST :

- `POST /restaurants` : créer un restaurant. On ne spécifie pas d'ID car il n'existe pas encore!
- `DELETE /restaurants/487499` : supprimer le restaurant avec l'ID `487499`.
- `GET /restaurants/9328986/reservations` : obtenir les réservations du restaurant `9328986`.

Bien entendu, on peut tout de même utiliser des query parameters si désiré.

### Code de statut

Les codes de statut sont regroupés par groupe de 100 afin d'indiquer leur signification. Chaque code indique comment le serveur a traité la requête. Voici les groupes de status importants, leur signification et quelques exemples :

- 200 à 299 : Succès.
    - `200` ou `Ok` : code de succès de base. Souvent retourné avec un body.
    - `201` ou `Created` : la ressource à été crée. Souvent retourné avec un header de type `Location` pour indiquer le path vers la nouvelle ressource.
    - `204` ou `No Content` : Même chose que `200`, mais sans body.
- 400 à 499 : Erreur de la part du client.
    - `400` ou `Bas Request` : code d'erreur client de base. Souvent utilisé pour des paramètres manquants ou invalides.
    - `404` ou `Not Found` : le path n'existe pas.
    - `405` ou `Method Not Allowed` : le path existe, mais pas pour cette méthode.
    - `415` ou `Media Type Not Supported` : le type de body n'est pas supporté par le serveur.

## Partie 2 - Jersey

Jersey est une librarie Java qui nous permet de définir une **API** (une porte d'entrée vers notre application) Web en utilisant HTTP. À l'aide de quelques annotations Java, on peut associer des routes à des classes et fonctions Java, extraire des headers, retourner un body, etc. Elle est déjà installée dans votre projet initial.

### Recevoir une requête

Pour recevoir une requête, on doit associer une route (path + méthode) à une fonction. Ensuite, dans les arguments de la fonction, on peut y extraire différentes informations, comme les headers et le body. Voici une liste des annotations Jersey de fonction qui seront utiles :

- `@Path("/le-path")` : définit un path associé à la fonction qui suit
    - Un path peut contenir des portions dynamiques (des **path parameters**). Elles sont identifiées entre `{}`. Ex: `@Path("/employees/{id}")`.
- `@GET`, `@POST`, `@DELETE`, etc. : définit la méthode associée à la fonction qui suit
- `@Consumes(MediaType)` : Indique quel format le body de la requête doit avoir

Voici les annotations Jersey de variables qui seront utiles :

- `@PathParam("nom-du-path-param")` : Extrait le path param du nom spécifié et le stocke dans la variable qui suit
- `@QueryParam()`
- `@HeaderParam("nom-du-header")` : Extrait le header du nom spécifié et le stocke dans la variable qui suit

Pour recevoir le body et l'interpréter selon une classe Java spécifique, il suffit de le recevoir en argument de la fonction, sans aucune annotation.

Exemple de placement des annotations :

```java
class EmployeeResource {
  @Path("/employees/{id}")
  @GET
  public void getEmployee(@PathParam("id") String id) {
    // ...
  }

  @Path("/employees")
  @POST
  @Consumes(MediaType.APPLICATION_JSON)
  public void createEmployee(EmployeeBody body) {
    // ...
  }
}
```

### Renvoyer une réponse

Pour renvoyer une réponse, il suffit d'utiliser la classe `Response` de jersey. Elle agit à la fois comme une interface (type) de retour de la fonction et comme un builder (constructeur) de réponse HTTP. Utilisé comme un type de retour, `Response` prend un type générique, qui correspond au type du body retourné. Utilisé comme builder, il prend la structure suivante : `Response.status(status).entity(body).build()`. Différentes autres méthodes permettent de retourner des headers, ou des réponses plus standard comme `201 Created`.

De plus, si on retourne un body, il faudra ajouter une annotation `@Produces(MediaType)` à la fonction afin de spécifier le format du body de la réponse HTTP.

## Exercices

Afin de mettre en pratique, utilisez le logiciel Postman (ou équivalent) afin d'exécuter des requêtes HTTP sur votre serveur.

### 1. Recevoir une requête simple

Créez une première fonction et annotez-la avec Jersey afin de recevoir la route suivante :

```
GET /products
```

Pour vous aider, utilisez le débuggueur d'IntelliJ afin de savoir si la fonction a été executée.

> Vous aurez peut-être besoin de mettre une ligne bidon dans votre fonction afin de pouvoir y mettre un breakpoint.

### 2. Recevoir des paramètres

Tentez maintenant d'extraire le query parameter `sort` de la route suite :

```
GET /products?sort=popular
```

Tentez également d'envoyer des headers avec Postman et de les recevoir dans votre fonction.

Tentez ensuite de recevoir un query parameter avec la route `GET /products/{id}`.

### 3. Recevoir un body

Envoyez maintenant la requête suivante :

`POST /products`

Avec le body JSON suivant :

```json
{
  "title": "Pink Hairbrush",
  "description": "Very sturdy",
  "price": 4.99,
  "sold": false
}
```

Tentez d'extraire et convertir le body en objet Java. Il vous faudra d'abord créer une classe Java avec les mêmes propriétés et les bons types.

Une fois réussi, ré-exécutez Postman en enlevant le paramètre `title`, puis le paramètre "price", et observez le résultat. Est-ce qu'une erreur est soulevée? Ou est-ce que le paramètre est `null`? Dans quel cas est-ce que chacun des comportements survient?

### 4. Renvoyer une réponse simple

Tentez maintenant de renvoyer un status `404` pour la route `GET /products/{id}`

### 5. Renvoyer une réponse avancée

Essayez de renvoyer un header. Il n'est pas obligé d'être standard.

### 6. Renvoyer un body

Renvoyez maintenant un body pour une de vos routes. Essayez avec :
- un objet simple
- une liste d'objets
- une liste d'objets composée de sous-objets
- un objet contenant seulement des types primitifs (string, int, boolean, etc.)
- un objet contenant des classes Java plus complèxes (DateTime, Optional, Iterator, etc.)

Notez comment la traduction de Java vers JSON se fait. Notez également les types qui semblent retourner une valeur correcte, ceux qui retournent des valeurs étranges et ceux qui lancent des erreurs.
