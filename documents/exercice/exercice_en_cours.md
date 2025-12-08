PREFIX dbr: <https://dbpedia.org/resource/>
PREFIX dbo: <https://dbpedia.org/ontology/>
SELECT ?person ?object 
WHERE {
    dbr: List_of_linguists ?p ?person.
?person s dbo:Person;

