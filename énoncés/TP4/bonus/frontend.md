# Frontend (Bonus)

En guise de récompense pour votre dur labeur, votre ami a décidé de vous créer un frontend pour votre API, permettant 
ainsi de faire fonctionner l'application sur votre réseau local (et/ou de la déployer si vous le souhaitez).

## Étapes pour intégrer le frontend

### Ajouter le filtre CORS à votre backend

Ce filtre CORS permet d'accepter n'importe quelle requête de n'importe quel client (à ne pas faire en production).

```java
// glo2003/lib/http/filter/CorsFilter.java
package ca.ulaval.glo2003.lib.http.filter; // Modifier le package selon l'endroit où vous mettez la classe

import jakarta.ws.rs.container.ContainerRequestContext;
import jakarta.ws.rs.container.ContainerResponseContext;
import jakarta.ws.rs.container.ContainerResponseFilter;
import jakarta.ws.rs.ext.Provider;
import java.io.IOException;

@Provider
public class CorsFilter implements ContainerResponseFilter {

    @Override
    public void filter(ContainerRequestContext requestContext, ContainerResponseContext responseContext)
            throws IOException {

        responseContext.getHeaders().add("Access-Control-Allow-Origin", "*");
        responseContext.getHeaders().add("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
        responseContext.getHeaders().add("Access-Control-Allow-Headers",
                "Content-Type, Authorization, Member");

        if (requestContext.getMethod().equalsIgnoreCase("OPTIONS")) {
            responseContext.setStatus(200);
        }
    }
}
```

Ajoutez-le en tant que middleware à votre serveur HTTP.

```java

final ResourceConfig rc = new ResourceConfig()
                .register(new HealthResource())
                // Autres ressources
                .register(new CorsFilter());

GrizzlyHttpServerFactory.createHttpServer(URI.create(url), rc);
```

### Modifier le docker compose

Votre ami a été suffisamment gentil pour héberger l’image du frontend sur Docker Hub, vous avez donc simplement besoin de
la _puller_.

Voici un fichier `docker-compose.yaml` fonctionnel :

```yaml
services:
  api-local:
    build: .
    environment:
      PORT: 80
      MONGO_CLUSTER_URL: mongodb://root:example@mongo:27017
      MONGO_DATABASE: groups
    ports:
      - 8081:80
    command: mvn exec:java -D persistence=mongo

  api-remote:
    image: ghcr.io/test-glo-2003/test_cd:remise3 # Utlisez votre déploiement
    environment:
      PORT: 80
      MONGO_CLUSTER_URL: mongodb://root:example@mongo:27017
      MONGO_DATABASE: groups
    ports:
      - 8082:80
    command: mvn exec:java -D persistence=mongo

  mongo:
    image: mongo:8
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    ports:
      - 27017:27017
    volumes:
      - mongo:/data/db

  frontend:
    image: dferland1/frontend
    environment:
      API_URL: http://localhost:8081
    ports:
      - "3000:3000"
    depends_on:
      - api-local

volumes:
  mongo:
```

### Desktop Browser

Faire `docker compose up` et simplement vous diriger ici: [http://localhost:3000](http://localhost:3000) et l'app devrait être fonctionnelle!

### Mobile

Pour rouler sur mobile, vous devez trouver l'adresse IP de votre réseau Wi-Fi (elle commence habituellement par
192.168.x.x).
Pour ce faire, entrez soit `ifconfig` (Mac et Linux) ou `ipconfig` (Windows) dans un terminal pour la trouver.
Ensuite, veuillez changer la variable d'environnement `API_URL` : `http://<votre-adresse-ip>:8081`

Si tout se passe bien, vous pouvez maintenant naviguer à cette adresse avec votre téléphone pour accéder à l'application Splitul!

Vous pouvez donc laisser une instance rouler constamment dans votre appartement pour faire le partage des paiements avec vos colocs ou partenaires.

### Code

Le code du frontend ce trouve ici: [https://github.com/glo2003/splitul-frontend](https://github.com/glo2003/splitul-frontend)

Amusez-vous avec!
