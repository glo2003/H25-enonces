# Projet GLO2003 : SplitUL - TP3

- **📅 Fin: 1 avril 2024 à 23h59**
- **Tag: `remise3`**

> Toutes les **questions** des exercices sont à répondre dans le fichier `exercices/tp3.md`, sauf lorsque spécifé autrement.

## Requis fonctionnels

- [Historique des dépenses](fonctionnels/8.historique-des-depenses.md)
- [Régler compte](fonctionnels/9.regler-compte.md)
- [Modification à supprimer groupe](fonctionnels/10.modification-supprimer-groupe.md)
- [Ajouter header d'authentification](fonctionnels/11.ajouter-header-authentification.md)

## Requis de processus

- [CD](processus/cd.md)
- [Planification](processus/planification.md)
- [Rétrospective](processus/retro.md)
- [Stories](processus/stories.md)

## Requis techniques

- [Architecture](techniques/architecture.md)
- [Base de données](techniques/db.md)
- [Déclaration utilisation IA](techniques/declaration-IA.md)
- [Tests](techniques/tests.md)

## Restrictions importantes

Pour assurer le bon fonctionnement des outils de correction automatisés, vous **ne devez pas modifier** les éléments suivants :

- **La route GET `/health`** : Cette route est utilisée pour vérifier si votre serveur démarre correctement.
- **L'URL `0.0.0.0`** : Cela rend votre serveur accessible sur un réseau local (notez que `localhost` ne fonctionne pas toujours).
- **Le port `8080`** : Utilisez ce port pour votre serveur. Vous pourrez utiliser la variable d'environnement `PORT` à partir du TP3.
- **Le fichier `Dockerfile`** : Ce fichier est essentiel pour démarrer votre serveur.

## Instructions pour les screenshots

Pour fournir les screenshots nécessaires au projet, vous avez deux options :

1. Héberger les images sur un service externe :
- Utilisez un service d'hébergement d'images qui génère des liens directs accessibles publiquement.
- Incluez ces liens dans votre fichier markdown (exercices/tp1.md).

2. Ajouter les images dans votre repository (pas avec un drag and drop) :
- Placez les images directement dans un dossier dans votre repository (attention à la taille).
- Utilisez des liens relatifs dans votre markdown (par exemple : ./images/abc.png).

## Critère d'évaluation et pondération

### Section Qualité

| Critère        | Pondération | Note     | Note Pondérée |
|----------------|-------------|----------|---------------|
| Processus      | 20%         | 100.00%  | 20.00%        |
| Clean code     | 20%         | 100.00%  | 20.00%        |
| Implémentation | 30%         | 100.00%  | 30.00%        |
| Tests          | 30%         | 100.00%  | 30.00%        |
| **SOUS-TOTAL** |             |          | **100.00%**   |

---

### Résumé

| Section    | Pondération | Note     | Note Pondérée |
|------------|-------------|----------|---------------|
| Qualité    | 70%         | 100.00%  | 70.00%        |
| Exercices  | 10%         | 100.00%  | 10.00%        |
| Features   | 20%         | 100.00%  | 20.00%        |
| Pénalités  | -10%        | 0.00%    | 0.00%         |
| **TOTAL**  |             |          | **100.00%**   |
