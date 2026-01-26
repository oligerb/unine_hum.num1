https://en.wikipedia.org/wiki/Leonard_Bloomfield  URL

https://dpedia.org/resource/Leonard_Bloomfield   URI IRI 

PREFIX dbr: <https://dbpedia.org/resource/>
SELECT*
WHERE
{
https://dpedia.org/resource/Leonard_Bloomfield  ?p?o
}
--> fonctionne pas car manque <...>

PREFIX dbr: <https://dpedia.org/resource/>
SELECT*
WHERE
{
dbr:Leonard_Bloomfield ?p?o
}
PREFIX rdf: <https://www.w3.org/1999/02/22-rdf-syntax-ns#> 

identifiant de la classe:
PREFIX dbo: <https://dbpedia.org/onthology/>

PREFIX dbr: <https://dbpedia.org/resource/>
PREFIX rdf: <https://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX dbo: <https://dbpedia.org/ontology/>
SELECT* (COUNT(*)AS ?number) 
WHERE
{
?person rdf:type dbo:Person
}



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


INSERT {?person rdfs:label ?label;
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



PREFIX dbo: <http://dbpedia.org/ontology/> 

SELECT (COUNT(*) as ?number)
WHERE {?s a dbo:Person}


PREFIX dbo: <http://dbpedia.org/ontology/> 
SELECT ?s ?p ?o
WHERE {?s a dbo:Person;
        ?p ?o.
FILTER (?o != dbo:Person)
    }
ORDER BY ?s ?p
LIMIT 100

### importer les triplets de wiki


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



PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>

SELECT (COUNT(*) AS ?number) WHERE {?s a dbo:Person; owl:sameAs ?o. }



PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>


SELECT *
WHERE {
  ?s owl:sameAs ?wdPerson;
          a dbo:Person.
  FILTER (CONTAINS(STR(?wdPerson), 'wikidata'))        
  SERVICE <https://query.wikidata.org/sparql> {
            ?wdPerson wdt:P269 ?idRef.
            BIND(URI(CONCAT('http://www.idref.fr/', ?idRef, '/id')) as ?uriIdRef)
      }     
}
LIMIT 10



select ?p ?o
where {
    SERVICE <https://data.idref.fr/sparql> {
            <http://www.idref.fr/032799128/id> ?p ?o.
      }     
      }
### -->ici personne prend la place de objet donc on voit ce qui entre --> donc par exemple ou ils sont cités!!
select ?p ?o
where {
    SERVICE <https://data.idref.fr/sparql> {
          ?p ?o <http://www.idref.fr/032799128/id> 
      }     
      }




      PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

# CONSTRUCT {?person owl:sameAs ?uriIdRef.}
INSERT {?person owl:sameAs ?uriIdRef.}
    WHERE {

      ?person owl:sameAs ?wdPerson;
            a dbo:Person.
    FILTER (CONTAINS(STR(?wdPerson), 'wikidata'))        
    SERVICE <https://query.wikidata.org/sparql> {
              ?wdPerson wdt:P269 ?idRef.
              BIND(URI(CONCAT('http://www.idref.fr/', ?idRef, '/id')) as ?uriIdRef)
        }  
  }



  PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>


SELECT ?person ?idrefPerson ?p ?o
WHERE {
        ?person owl:sameAs ?idrefPerson;
            a dbo:Person.
    FILTER (CONTAINS(STR(?idrefPerson), 'idref'))  
     
  SERVICE <https://data.idref.fr/sparql> {
            ?idrefPerson ?p ?o.
      }     
  }
ORDER BY ?person
LIMIT 100


PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>


SELECT ?p (count(*) as ?number)
WHERE {
        ?person owl:sameAs ?idrefPerson;
            a dbo:Person.
    FILTER (CONTAINS(STR(?idrefPerson), 'idref'))  
     
  SERVICE <https://data.idref.fr/sparql> {
            ?idrefPerson ?p ?o.
      }     
  }
GROUP BY ?p
ORDER BY DESC(?number)



PREFIX dbr: <http://dbpedia.org/resource/>
PREFIX dbo: <http://dbpedia.org/ontology/> 
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>


SELECT ?p (count(*) as ?number)
WHERE {
        ?person owl:sameAs ?idrefPerson;
            a dbo:Person.
    FILTER (CONTAINS(STR(?idrefPerson), 'idref'))  
     
  SERVICE <https://data.idref.fr/sparql> {
            ?s ?p ?idrefPerson.
      }     
  }
GROUP BY ?p
ORDER BY DESC(?number)