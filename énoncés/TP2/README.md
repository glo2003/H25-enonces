# Projet GLO2003 : SplitUL - TP2

- **📅 Fin: 4 mars 2025 à 23:59**
- **Tag: `remise2`**

> Toutes les **questions** des exercices sont à répondre dans le fichier `exercices/tp2.md`, 
> sauf lorsque spécifié autrement.

## Requis fonctionnels (features)

- [Ajouter un membre au groupe](fonctionnels/5.ajouter-membre-groupe.md)
- [Ajouter une dépense](fonctionnels/6.ajouter-depense-groupe.md)
- [Lister les membres d'un groupe](fonctionnels/7.lister-membres-groupe.md)

## Requis de processus

- [CI](processus/ci.md)
- [Planification](processus/planification.md)
- [Retrospective](processus/retrospective.md)

## Requis techniques

- [Architecture](techniques/architecture.md)
- [Clean Code](techniques/clean-code.md)
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

2. Ajouter les images dans votre repository :
- Placez les images directement dans votre repository (attention à la taille).
- Utilisez des liens relatifs dans votre markdown (par exemple : ./images/abc.png).

## Critère d'évaluation et pondération

### Section Qualité

| Critère        | Pondération | Note     | Note Pondérée |
|----------------|-------------|----------|---------------|
| Processus      | 20%         | 100.00%  | 20.00%        |
| Clean code     | 30%         | 100.00%  | 30.00%        |
| Implémentation | 20%         | 100.00%  | 20.00%        |
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
