[← Retour](../README.md)

# Conventions Git

Vous commencez un nouveau projet, il est donc impératif de mettre en place des bonnes conventions en équipe.

## Fichiers ignorés

Ajoutez un fichier `.gitignore` à la racine de votre projet. Ce dernier **doit** suivre les meilleures pratiques en terme de fichiers ignorés. Vous trouverez beaucoup d'information sur le Web à ce sujet. On veut notamment ignorer :

- Les configurations *personnelles* (mais pas celles d'équipe!)
- Les fichiers contenant des *path* personnels (Ex: `/User/Steph/Documents/glo2003/le_projet`)
- Les fichiers auto-générés
- Les fichiers contenant des *secrets* (mots de passes, clés, etc.)
- Les *builds* (fichiers compilés)

Certaines configurations standards sont disponibles sur le Web, mais vous **devez** vous assurer de bien l'adapter à votre projet (et de **citer vos sources!**).

## Nommage des commits

Vous devez suivre une convention pour l'écriture et le contenu des commits. Vous pouvez vous inspirer de pratiques populaires existantes si vous le désirez. On vous demande de **décrire votre convention de commits** dans le fichier `exerices/tp1.md`. Assurez-vous d'**indiquer vos sources** si vous vous inspirez d'ailleurs. On cherche notamment à savoir :

1. Comment nommer les commits selon leur type/section/grosseur/acteur/etc.
2. Quoi et quand commiter?

Vous n'êtes pas obligé de suivre un standard, mais vos méthodes *doivent* être **cohérentes**.

## Stratégie de branchage

Vous devez établir une convention pour la gestion et le nommage des branches. Vous pouvez vous inspirer de pratiques populaires existantes si vous le désirez. On vous demande de **décrire votre stratégie de branchage** dans le fichier `exerices/tp1.md`. Assurez-vous d'**indiquer vos sources** si vous vous inspirez d'ailleurs. On cherche notamment à savoir :

1. Quelles sont les branches *de base* (qui sont communes et qui existeront toujours) et quels sont leurs rôles (chacune)?
2. Quelle branche est *LA* branche principale (contenant le code officiellement intégré et pouvant être remis)?
3. Quand créer une nouvelle branche?
4. Quand faire une demande de changement / d'intégration (pull request / merge request) et sur quelle branche la faire?

Voici quelques exemples de stratégies que vous pouvez utiliser ou pour vous inspirer :
- [Git Flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
- [Github Flow](https://githubflow.github.io/)
- [Gitlab Flow](https://docs.gitlab.com/ee/topics/gitlab_flow.html)
- Trunk based ([1](https://cloud.google.com/architecture/devops/devops-tech-trunk-based-development) et [2](https://www.atlassian.com/continuous-delivery/continuous-integration/trunk-based-development))

Vous n'êtes pas obligé de suivre un standard, mais vos méthodes *doivent* être **cohérentes**.
