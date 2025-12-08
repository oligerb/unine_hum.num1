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

