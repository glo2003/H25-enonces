[← Retour](../README.md)

# Intégration continue (CI)

Afin d'augmenter la confiance de vos intégrations logicielles, vous devez mettre en 
place un pipeline d'intégration continue (CI). Pour ce faire, vous devez utiliser 
Github Actions, qui est intégré à Github. Votre pipeline doit avoir au moins les 
étapes séparées et explicites suivantes :

1. Vérification du formatage
2. Compilation
3. Tests

Chacune de ces étapes **doit** faire échouer le pipeline si celle-ci échoue. 
Ex: S'il y a une erreur de formatage, le pipeline doit échouer.

Vous devez également satisfaire les exigences suivantes :

1. Mise en place de la bonne version de Java
2. Utilisation de la cache pour les dépendances Maven
3. Exécution du pipeline sur tous les commits de pull requests, ainsi que sur tous 
les commits de chaque branche principale (ex: `dev`, `master`, etc.)

Il vous est fortement suggéré de lire la [documentation](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions) de Github Actions.

## IMPORTANT

Vous disposez d'une limite de 2000 minutes d'exécution par mois 
(sur `ubuntu`, 2x moins sur `windows` et 10x moins sur `macos`) par équipe pour le 
pipeline CI. Afin d'éviter de dépasser les minutes permises, vous pouvez configurer 
une limite de temps par exécution. Normalement, une exécution ne devrait jamais 
dépasser 5 minutes (dans votre cas).

Pour plus de détails : https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobsjob_idtimeout-minutes
