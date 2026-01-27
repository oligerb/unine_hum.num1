# Mes requêtes SPARQL

## Sortir les universités/organisations fréquentées

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>
SELECT DISTINCT ?person (?almaMater AS ?organisation) 
                               ("almaMater" as ?membership_type) (2 AS ?fk_sparql_query)
                              (STR("Importation 21 janvier 2026") as ?metadata)
WHERE { 
dbr:List_of_linguists ?p ?person.
?person a dbo:Person;
        dbo:birthDate ?birthDate ;
    dbo:almaMater ?almaMater.
    BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
    FILTER ( ?birthYear > 1770)
}

## Sortir les personnes de la liste de linguistes

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?person_uri (STR(?label) AS ?persName) ?birthYear
WHERE { 
    dbr:List_of_linguists ?p ?person_uri.
    ?person_uri a dbo:Person;
            dbo:birthDate ?birthDate;
            rdfs:label ?label.
    BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)

}
ORDER BY ?birthYear

(avec éventuellement "FILTER ( ?birthYear > 1770
            && LANG(?label) = 'en')" si l'on veut mettre une limite et prendre uniquement les personnes avec des dates de naissances suppérieurs à 1770)

## Sortir les appartenances à des universités ou institutions

PREFIX dbr: <http://dbpedia.org/resource/>
        PREFIX dbo: <http://dbpedia.org/ontology/>
        SELECT DISTINCT    ?organisation (STR(?organisationLabel) AS ?label)
    (group_concat(DISTINCT  ?type, ',') as ?types)
        (4 AS ?fk_sparql_query)
        (STR("Importation 21 janvier 2026") as ?metadata)
        WHERE { 
        {
        dbr:List_of_linguists ?p ?person.
        ?person a dbo:Person;
                dbo:birthDate ?birthDate ;
            dbo:institution ?organisation.
    ?organisation rdfs:label ?organisationLabel
            BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
            BIND('institution' as ?type)
            FILTER ( ?birthYear > 1770 && LANG(?organisationLabel)='en')
    }
    UNION
    {
        dbr:List_of_linguists ?p ?person.
        ?person a dbo:Person;
                dbo:birthDate ?birthDate ;
            dbo:almaMater ?organisation.
    ?organisation rdfs:label ?organisationLabel
            BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
            BIND('almaMater' as ?type)
            FILTER ( ?birthYear > 1770 && LANG(?organisationLabel)='en')
    }
        }
    GROUP BY ?organisation ?organisationLabel         

