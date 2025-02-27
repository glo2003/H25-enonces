[← Retour](../README.md)

# Connexion à une base de données externe

## Description

Pour stocker les informations sur le long terme, il est nécessaire de se connecter à une base de données externe. Dans 
ce cadre, l'intégration avec une base de données [MongoDB](https://www.mongodb.com/) est requise. L'utilisation de l'ODM (Object Document Mapper)
[Morphia](https://morphia.dev/landing/index.html) facilitera et automatisera plusieurs tâches liées à l'interaction avec cette base de données.

## Sélection de base de données

Au démarrage de l'application, la **propriété système** (*system property*) `persistence` permet de sélectionner le type 
de persistance à utiliser. Vous devez donc développer deux implémentations pour chaque fonction de persistance : une pour 
la persistance en mémoire et une autre pour MongoDB. La propriété système vous permet de choisir l'une ou l'autre des 
deux options au démarrage. Les valeurs possibles pour cette propriété sont :

- `inmemory` (par défaut)
- `mongo`

Si la propriété n'est pas spécifiée, vous devez utiliser la version `inmemory`.

## Installation

Vous devez choisir entre installer une instance locale de MongoDB directement sur votre ordinateur ou utiliser une 
version conteneurisée via Docker et `docker compose`.

### Option 1 : Instance locale

Pour ce faire, vous devez [installer MongoDB](https://www.mongodb.com/try/download/community) localement. Nous utiliserons 
la dernière version à jour (8+) pour le projet.

### Option 2 (préférable) : Version conteneurisée (Docker)

Pour ce faire, vous devrez d'abord installer [Docker](https://www.docker.com/products/docker-desktop/). Utilisez ensuite cette [configuration docker-compose](./docker-compose.yml) 
afin de démarrer une version conteneurisée de MongoDB. Vous aurez simplement à exécuter `docker compose up` dans un 
terminal pour démarrer le serveur (ajoutez `-d` pour que l'exécution soit en arrière-plan).

Avec cette configuration, l'URL de connexion à la base de données (`MONGO_CLUSTER_URL`) est `mongodb://root:example@localhost:27017`. 
Vous pouvez spécifier n'importe quelle valeur pour la base de données `MONGO_DATABASE`, qui sera automatiquement créée.

## Variables d'environnement

> ⚠️ Ces variables d'environnement sont **requises** pour le mode `persistence=mongo` et seront utilisées pour la 
> correction automatique. On doit pouvoir y spécifier n'importe quelle valeur lors du démarrage de l'application.

| Nom                        | Description                                                                                                                                                          |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `MONGO_CLUSTER_URL` | URL complet utilisé pour la connexion au cluster de bases de données. Contient le protocole, le *username*, le *password*, le *host*, le *port* et possiblement les options. |
| `MONGO_DATABASE`    | Base de données à laquelle se connecter.                                                                                                                              |

## Connexion

La connexion au cluster MongoDB nécessite d'abord la création d'un client Mongo (com.mongodb.client.MongoClients), 
suivie de la création d'un datastore Morphia (dev.morphia.Datastore). Les documentations suivantes fournissent les 
informations nécessaires à cette configuration :

- Documentation [MongoDB Driver](https://docs.mongodb.com/drivers/java/sync/v4.5/fundamentals/connection/connect/#std-label-connect-to-mongodb)
- Documentation [Morphia](https://morphia.dev/morphia/2.2/quicktour.html#_setting_up_morphia)

## Morphia

Morphia permet de *mapper* vos classes Java vers des objets représentatifs simples ("documents") pour la base de données. 
Il sera donc primordial de respecter le même principe que pour vos réponses du UI, c'est-à-dire de créer des classes 
propres aux documents MongoDB qui contiendront des champs de **primitives seulement** ainsi que les annotations Morphia. 
La documentation contient beaucoup d'informations pertinentes.

## Conseils et astuces

### Modifier le timeout de connexion

Dans le cas d'une connexion non fonctionnelle, le driver MongoDB attendra 30 secondes avant d'échouer, ce qui peut être 
particulièrement long. Il est donc possible de configurer le client MongoDB à l'aide du builder `MongoClientSettings`. 
Afin de réduire le timeout, vous pouvez modifier les paramètres de `serverSelectionTimeout` (dans les options de `cluster`) 
et de `maxConnectionIdleTime` (dans les options de `connectionPool`). Vous aurez alors également besoin de configurer 
l'URL à l'aide du builder. Faites attention à ne pas trop réduire ce timeout, car la connexion peut parfois prendre quelques secondes.
