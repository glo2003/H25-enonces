[← Retour](../README.md)

# Déploiement continu (CD)

Vous devez *packager* votre application et la téléverser dans un registre afin de pouvoir facilement, uniformément et 
rapidement utiliser votre application dans n'importe quel environnement.

## *Packaging* avec Docker

En Java, il existe plusieurs façons de *packager* et distribuer une application. La méthode classique consiste à générer 
un fichier `.jar`, qui correspond à une archive précompilée du code. Ce fichier est ensuite interprétable sous différents 
environnements Java. Cependant, les étapes pour construire un JAR sont souvent obscures et les dépendances ne sont pas 
toujours bien liées. De plus, les nouvelles versions majeures de Java sont de plus en plus courantes et même si la 
majorité du code reste *backward-compatible*, ce n'est pas toujours le cas.

Ainsi, afin de mieux assurer le comportement de l'application, vous la déploierez dans une image Docker.

> ⚠️ Notez que le fichier de configuration `Dockerfile` vous est déjà fourni et **vous devez le modifier comme ceci :**

```
FROM maven:3-amazoncorretto-21

WORKDIR /app

COPY pom.xml .
RUN mvn --batch-mode exec:java || exit 0

COPY . .
RUN mvn --batch-mode compiler:compile

CMD ["mvn", "--batch-mode", "--offline", "exec:java"]
```
> ⚠️ Le fichier doit être copié-collé et être exactement identique à celui fourni ici. L'option batch mode a été ajoutée pour rendre 
> les logs plus lisibles, et `COPY src src` a été remplacé par `COPY . .` afin d'inclure également les fichiers de configuration
> utilisés par certaines équipes.

## Déploiement (Github Actions)

La construction et le déploiement de votre image Docker doivent se faire à l'aide d'un pipeline automatisé avec 
**GitHub Actions**. Votre déploiement doit s'effectuer :

- À chaque nouveau commit sur votre branche principale
- À chaque nouveau tag
- Manuellement (déploie le dernier commit)

Il est également **absolument impératif** que l'image :

- Soit publiée sur le registre `ghcr.io` (celui de GitHub).
- Possède le même nom que le repository (en minuscules).
- Soit *taguée* avec le hash du commit et s'il y a lieu le nom du tag Git.

Voici une ressource qui pourrait vous aider : <https://docs.github.com/en/actions/publishing-packages/publishing-docker-images>.

## Variables d'environnement

Lors du déploiement, il est impossible de prédire à l’avance sur quel port l’application pourra s’exécuter. 
Cette valeur est souvent déterminée dynamiquement par le *runner* (serveur hôte) en fonction des autres applications 
déjà en cours d’exécution. Vous devez donc récupérer la variable d’environnement `PORT` et démarrer l’application sur 
ce port. Si cette variable n’est pas définie, utilisez la valeur `8080` par défaut. Pour l’adresse `host`, utilisez toujours `0.0.0.0`.
