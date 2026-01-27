# Problématique

Dans le cadre du cours " Humanités numériques 1: Production et gestion des données", j'ai choisi de m'intéresser aux linguistes. Il s'agit donc de proposer, dans une démarche exploratoire, un modèle permettant de visualiser des listes de presonnes (ici, des linguistes) et d'analyser leur origines, leur appartenances à des institutions/organisations et des relations entre différents individus. 
Dans une perspective prosopographique, j’adopterai une démarche de collecte systématique des caractéristiques biographiques, institutionnelles et scientifiques des linguistes. 
L’objectif est de dégager des tendances communes dans les trajectoires et les liens entre linguistes, afin de saisir les logiques qui structurent leur milieu professionnel.
L’exploitation de ces données biographiques me permettra d’obtenir une vue d’ensemble structurée, à partir de laquelle je pourrai ensuite répondre aux questions de recherche formulées ci‑dessous.

 
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

```sql
CREATE VIEW vue_person_organisation AS
SELECT p.name , o. organisation_name
FROM membership m
JOIN person p on p.pk_person =m.fk_person 
JOIN organisation o on o.pk_organisation = m.fk_organisation;


CREATE VIEW person_birth AS 
SELECT p.pk_person, p.name, b.birth_place, b.birth_date 
FROM Person p 
JOIN Birth b 
ON p.pk_person = b.fk_person;


CREATE VIEW occurence_uni AS
SELECT o.organisation_name, COUNT(*) AS nb_occurrences 
FROM membership m 
JOIN organisation o ON o.pk_organisation = m.fk_organisation 
GROUP BY o.organisation_name 
ORDER BY nb_occurrences 
DESC;
