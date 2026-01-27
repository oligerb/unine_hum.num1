# Problématique
Dans le cadre du cours " Humanités numériques 1: Production et gestion des données", j'ai choisi de m'intéresser aux linguistes. Il s'agit donc de proposer un 

En adoptant une démarche exploratoire, il s’agit de proposer un modèle du champ scientifique de la linguistique (en mobilisant les notions de champ, d’habitus et de capital chez Pierre Bourdieu), c’est‑à‑dire une représentation simplifiée de la structure de ce domaine disciplinaire et de son évolution dans le temps. L’objectif est d’analyser les profils socio‑démographiques et les positions intellectuelles des agents, leurs appartenances institutionnelles, ainsi que les réseaux de relations qui se tissent entre chercheurs, écoles de pensée et organisations académiques. Il s’agira également de modéliser les transformations historiques de cette structure, en mettant en évidence les dynamiques de consolidation, de concurrence ou de recomposition des courants linguistiques. Dans une perspective prosopographique, nous collecterons systématiquement les caractéristiques biographiques, institutionnelles et scientifiques des linguistes afin de dégager des profils types, des trajectoires professionnelles et des configurations relationnelles révélatrices du fonctionnement du champ.

## Questions de recherche

- Est-ce que les universités fréquantées impaquent-elles la notoriété des linguistes ?

- Quelles universités ou institutions reviennent le plus souvent dans les parcours des linguistes ?

- Quels sont les domaines de spécialisation les plus représentés ?

- Quels linguistes apparaissent comme des figures centrales ? (par nombre de citations)

- Quels pays ont le plus de linguistes répertoriés ?

- Quels linguistes ont écrit le plus grand nombre d'articles ou d'ouvrages ?

- Est-ce que les linguistes les plus célébres ont des parents avec un niveau de formation élevé ?

## Les informations à collecter

- #### Origine 
- Profession des parents
- #### Formation 
- #### Appartenance à des institutions
- Publications

## SQL

Afin de gagner du temps, j'ai crée trois vues, qui me permettent d'accéder facilement à l'information sans devoir écrire la requête en entier (ou par le bouton "vues"). Il y'a d'abord `SELECT * FROM vue_person_organisation`qui me permet d'avoir toutes les personnes et les organisations dont elles ont été membres. (dans mon cas, ce sont uniquement les écoles/universités)
`SELECT * FROM person_birth`qui permet de sortir les personnes, leur lieu de naissance ainsi que la date. 
et `SELECT * FROM occurence_uni`qui permet de voir le nombre d'occurences de chaque université.

# Requêtes
Pour ce faire j'ai utilisé les requêtes suivantes:

````CREATE VIEW vue_person_organisation AS
SELECT p.name , o. organisation_name
FROM membership m
JOIN person p on p.pk_person =m.fk_person 
JOIN organisation o on o.pk_organisation = m.fk_organisation;````

````CREATE VIEW person_birth AS 
SELECT p.pk_person, p.name, b.birth_place, b.birth_date 
FROM Person p 
JOIN Birth b 
ON p.pk_person = b.fk_person;````

````CREATE VIEW occurence_uni AS
SELECT o.organisation_name, COUNT(*) AS nb_occurrences 
FROM membership m 
JOIN organisation o ON o.pk_organisation = m.fk_organisation 
GROUP BY o.organisation_name 
ORDER BY nb_occurrences 
DESC;````
