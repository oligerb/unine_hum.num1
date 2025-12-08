https://ag1efpn0ahc5nur8.allegrograph.cloud/webview

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT ?person ?label
WHERE {
SERVICE <https://dbpedia.org/sparql> {
    dbr:List_of_linguists ?p ?person.
    ?person a dbo:Person;
            dbo:birthDate ?birthDate ;
        rdfs:label ?label.
        BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
        FILTER ( ?birthYear > 1770  && LANG(?label) = 'en')
    }
}

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>


CONSTRUCT  {?person rdfs:label ?label;
                    a dbo:Person;
  
                    dbo:birthYear ?birthYear.
           }
WHERE {
SERVICE <https://dbpedia.org/sparql> {
    dbr:List_of_linguists ?p ?person.
    ?person a dbo:Person;
            dbo:birthDate ?birthDate ;
        rdfs:label ?label.
        BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
        FILTER ( ?birthYear > 1770  && LANG(?label) = 'en')
    }
  
}

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>


INSERT  {?person rdfs:label ?label;
                    a dbo:Person;
  
                    dbo:birthYear ?birthYear.
           }
WHERE {
SERVICE <https://dbpedia.org/sparql> {
    dbr:List_of_linguists ?p ?person.
    ?person a dbo:Person;
            dbo:birthDate ?birthDate ;
        rdfs:label ?label.
        BIND(xsd:integer(SUBSTR(STR(?birthDate), 1, 4)) AS ?birthYear)
        FILTER ( ?birthYear > 1770  && LANG(?label) = 'en')
    }
  
}

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

SELECT ?person  ?wikidataUri
    WHERE {

    ?person a dbo:Person.

    SERVICE <https://dbpedia.org/sparql> {
        ?person owl:sameAs ?wikidataUri.
            FILTER (CONTAINS(STR(?wikidataUri), 'wikidata'))
        }
}

PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

# CONSTRUCT {?person owl:sameAs ?wikidataUri.}
INSERT {?person owl:sameAs ?wikidataUri.}
    WHERE {

    ?person a dbo:Person.

    SERVICE <https://dbpedia.org/sparql> {
        ?person owl:sameAs ?wikidataUri.
            FILTER (CONTAINS(STR(?wikidataUri), 'wikidata'))
        }
}


PREFIX dbo: <http://dbpedia.org/ontology/> 

SELECT ?s ?p ?o
WHERE {?s a dbo:Person;
        ?p ?o.
FILTER (?o != dbo:Person)
    }
ORDER BY ?s ?p