[← Retour](../README.md)

# Outils de métrique

Bien que des [outils d'analyses](./analysis.md) et des tests aient été mis en place, des bogues peuvent toujours survenir.
De plus, en pratique, les applications s'exécutent sur des serveurs distants où l'accès aux logs et aux débogueurs 
n'est pas toujours possible. Pour pallier ce problème, vous devez mettre en place Sentry, un outil permettant de 
détecter, rapporter et notifier les erreurs en production.

**Critères**

1. Doit rapporter **toutes** les erreurs de votre code, sauf celles générées par Jersey (ex: 404 pour une route inexistante). 
L'utilisation d'un *exception mapper* pourrait grandement vous aider.
2. Utilisez la variable d'environnement `SENTRY_DSN` pour la valeur du DSN, puisqu'il s'agit d'une **donnée sensible**.
3. Ne **pas** utiliser le plugin `sentry-maven-plugin`, car il pourrait bloquer la correction automatique (nécessite une clé d’API). 
Utilisez plutôt la dépendance `sentry` directement dans votre code.

Incluez des captures d'écran de rapports de bogues, à la fois **sommaires** et **détaillés**, dans votre fichier `exercices/tp4.md`.

Vous n'êtes pas tenu de corriger les problèmes identifiés, sauf s'ils font partie des critères d’évaluation indiqués dans 
les énoncés.
