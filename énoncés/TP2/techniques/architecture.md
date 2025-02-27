[← Retour](../README.md)

# Requis architecturaux

## Respect des couches

Vous devez séparer la couche logique de la couche présentative. Pour ce faire, créez 
de nouvelles classes qui extraient le contenu logique (vérifications, actions, etc.) 
en dehors des classes de ressources/api (Jersey). Liez ensuite les couches à l'aide 
de convertisseurs (transforme un objet logique en objet représentatif et vice-versa).

## Packages

Afin de bien organiser les classes, on vous demande également de choisir une 
**structure de packages**. Pour ce faire, recherchez des stratégies existantes 
sur le Web. On parle souvent de "vertical slicing vs. horizontal slicing". 
Quelques axes de séparations incluent :

- couches (api, domaine/logique, etc.)
- modules (groupe, etc.)
- type (requêtes, factories, etc.)

Certaines séparations seront plus adaptées et permettront au code d'évoluer plus 
facilement. Assurez-vous de bien faire vos recherches et d'en discuter en équipe!

Finalement, assurez-vous que les noms des packages suivent les conventions Java et Maven.

## Diagrammes

**Veuillez répondre dans le fichier exercices/tp2.md de votre repo.**

Afin de bien visualiser les dépendances entre vos classes et vos couches, vous devez 
fournir un diagramme d'architecture simplifié. Pour ce faire, voici quelques directives :

- Indiquez clairement la **couche** d'appartenance de chaque classe (ex: à l'aide de couleurs et d'une légende)
- Pas besoin des méthodes ni des attributs, seulement besoin des **noms des classes**
- Pas besoin des classes de bas niveau (ex: `Email`, `PhoneNumber`, `OwnerId`, etc.) sauf si vraiment pertinent
- N'inclure **aucune** classe que vous **n'avez pas crées** (ex: les classes de la librairie standard ou de Jakarta)
- Pour chaque classe, pointez à l'aide d'une flèche nommées chaque action vers les autres classes.
    - Exemples d'actions:
        - **utilise** (*uses*)
        - **reçoit** (*receives*)
        - **créer** (*creates*)
        - **trouve/sauvegarde** (*finds/saves*)
        - **se transforme en** (*maps to*)
        - **valide** (*validates*)
        - **modifie** (*modifies*)
        - **implémente** (*implements*)
    - Pensez aux actions générale et non pas aux actions spécifiques comme "modifie le nom"

Vous devez également, dans un court texte associé :

- Décrire les rôles des classes principales
- Expliquer vos choix
- Noter les endroits où les relations semblent suspectes et trouver des solutions potentielles

Autres conseils:

- Pas d'annotations UML, seulement des flèches et des boîtes de base
- Pour améliorer la lisibilité, vous pouvez faire 1 diagramme par module 
- (`Groupe`, etc.) ou par action principale (*création groupe*, *obtention groupe*, etc.). 
Par contre, plus vous séparez en petits diagrammes, plus vous cachez les problèmes potentiels de votre architecture.
- Évitez le plus possible les croisements et superpositions
- Exportez votre diagramme en PNG, de qualité suffisante pour être **très** lisible
- Français ou anglais, idéalement pas un mélange des deux
- Outil suggéré : <https://app.diagrams.net> (**pas** Visual Paradigm)

Exemple de diagramme pour une feature très simple de *gestion des utilisateurs* (incomplet) :

<div align="center">
<img src="https://user-images.githubusercontent.com/32545895/218632494-9c417121-49c1-45c1-97a4-427a9450e965.png" width="600px" alt="Diagramme architecture simplifié">
</div>
