# Projet GLO2003 : SplitUL  - TP4

- **📅 Fin: 25 avril 2024 à 23h59**
- **Tag: `remise4`**

> Toutes les **questions** des exercices sont à répondre dans le fichier `exercices/tp4.md`, sauf lorsque spécifé autrement.

## Requis fonctionnels

- [Vos stories](fonctionnels/story.md)

## Requis de processus

- [Rétrospective](processus/retrospective.md)
- [Planification](processus/planification.md)
- [Open Source](processus/open-source.md)

## Requis techniques

- [Outils d'analyse](techniques/analyse.md)
- [Architecture](techniques/architecture.md)
- [Déclaration IA](techniques/declaration-IA.md)
- [Outils de métrique](techniques/metriques.md)
- [Sécurité](techniques/securite.md)

## Restrictions importantes

Pour assurer le bon fonctionnement des outils de correction automatisés, vous **ne devez pas modifier** les éléments suivants :

- **La route GET `/health`** : Cette route est utilisée pour vérifier si votre serveur démarre correctement.
- **L'URL `0.0.0.0`** : Cela rend votre serveur accessible sur un réseau local (notez que `localhost` ne fonctionne pas toujours).
- **Le fichier `Dockerfile`** : Ce fichier est essentiel pour démarrer votre serveur.

## Instructions pour les screenshots

Pour fournir les screenshots nécessaires au projet, vous avez deux options :

1. Héberger les images sur un service externe :
- Utilisez un service d'hébergement d'images qui génère des liens directs accessibles publiquement.
- Incluez ces liens dans votre fichier markdown (exercices/tp4.md).

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
| Qualité    | 75%         | 100.00%  | 75.00%        |
| Exercices  | 15%         | 100.00%  | 15.00%        |
| Features   | 10%         | 100.00%  | 10.00%        |
| Pénalités  |             | 0.00%    | 0.00%         |
| **TOTAL**  |             |          | **100.00%**   |
