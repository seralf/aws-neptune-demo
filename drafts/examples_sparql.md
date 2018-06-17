

## generazione dati di prova

```
DROP GRAPH <file://mondial>
;

LOAD <file:///C:/veltune_graph/mondial.rdf>
INTO GRAPH <file://mondial>
;
```


## statistiche 

```
SELECT (COUNT(*) AS ?triples)

WHERE {

?s ?p ?o .

}

```




SELECT DISTINCT ?concepts

FROM <file://mondial>

WHERE {

?s a ?concepts .

}


## esempio: dettagli su continenti

PREFIX mnd: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *

FROM <file://mondial>

WHERE {

?uri a mnd:Continent .
?uri ?prp ?obj .

}

## esempio: continente America

PREFIX mnd: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *

FROM <file://mondial>

WHERE {

?uri a mnd:Continent .
?uri ?prp ?obj .
  
FILTER(?uri=<http://www.semwebtech.org/mondial/10/continent/America/>)

}

## ex: risorse legate direttamente ad Africa/

PREFIX mnd: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *
FROM <file://mondial>
WHERE {
  ?uri a mnd:Continent .
  ?uri ?prp ?obj .
  ?other ?prp_inv ?uri .
  FILTER(?uri=<http://www.semwebtech.org/mondial/10/continent/Africa/>)
}



## ex: describe di America

DESCRIBE <http://www.semwebtech.org/mondial/10/continent/Africa/>


## ex: JOIN + OPTIONAL

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mndm: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT * 
FROM <file://mondial>
WHERE {
  
  ?uri a mndm:Continent .
  ?uri ?prp ?obj .
  ?obj ?prp_prp ?prp_obj . # JOIN PROBLEM!
  FILTER(?uri=<http://www.semwebtech.org/mondial/10/continent/Africa/>)
  
}

no results!

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mndm: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT * 
FROM <file://mondial>
WHERE {
  
  ?uri a mndm:Continent .
  ?uri ?prp ?obj .
  OPTIONAL { ?obj ?prp_prp ?prp_obj . } # JOIN PROBLEM!
  FILTER(?uri=<http://www.semwebtech.org/mondial/10/continent/Africa/>)
  
}

ok! RIGHT JOIN

## ex: con blazegraph

http://localhost:9999/blazegraph/#explore:kb:%3Chttp://www.semwebtech.org/mondial/10/country/ANG%3E%3C/a%3E

PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX mndm: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?uri ?prp ?obj ?prp_inv ?other 
#?uri ?prp ?prp_inv 
FROM <file://mondial>
WHERE {
  
  ?uri a mndm:Continent .
  
  { ?uri ?prp ?obj . }
  UNION
  { ?other ?prp_inv ?uri . }
  
  #?other ?prp_inv ?uri .
  
  FILTER(?uri=<http://www.semwebtech.org/mondial/10/continent/Africa/>)
  
}



## ex: 01


PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT *
FROM <file://mondial>
FROM <file://mondial-meta>
WHERE {
  
  ?uri a mon:Country .
  
  { ?uri ?prp ?obj . }
  UNION
  { ?other ?prp_inv ?uri . }
  
}


## ex: is member + population 


PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>

SELECT DISTINCT ?org_code ?org_name ?country_name (SUM(?pop_value) AS ?population)
FROM <file://mondial>
FROM <file://mondial-meta>
WHERE {
  
  ?country_uri mon:isMember ?org_uri . 
  ?org_uri mon:abbrev ?org_code .
  ?org_uri mon:name ?org_name .
  
  ?country_uri mon:name ?country_name .
  ?country_uri mon:hadPopulation ?pop_uri .
  
  ?pop_uri mon:value ?pop_value .
  ?pop_uri mon:year ?pop_year .
  
  # FILTER (?org_uri=<http://www.semwebtech.org/mondial/10/organization/FAO/>)
  
}

GROUP BY ?org_code ?org_name ?country_name 
ORDER BY DESC(?population) ?country_uri


----
https://www.dbis.informatik.uni-goettingen.de/Mondial/mondial-ER.pdf
----

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?name ?located_in  

WHERE {

  ?located_uri a mon:Country .
  ?uri mon:name ?name .
  
  OPTIONAL {
    ?uri mon:locatedIn+ ?located_uri .
  	?located_uri mon:name ?located_in .
  }
  
}
LIMIT 10000

----

## ex: fiumi in laghi 

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?river_uri (COUNT(?lake_uri) AS ?lakes)

WHERE {

  ?river_uri mon:flowsThrough+ ?lake_uri . #attraversa

}
GROUP BY ?river_uri 
ORDER BY DESC(?lakes) ?river_uri



----

# mari 

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *  

WHERE {

#?uri mon:flowsInto ?obj .
  
?uri <http://www.semwebtech.org/mondial/10/meta#mergesWith>* ?obj .

}


----

# acque

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *  

WHERE {

?uri <http://www.semwebtech.org/mondial/10/meta#flowsInto>+ ?sea_uri .
?sea_uri a mon:Sea .

}

ORDER BY ?uri 

-- v2 

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT *  

WHERE {

?uri mon:flowsInto+ ?sea_uri .
?sea_uri a mon:Sea .

}

ORDER BY ?uri 

----

## ex: lake water into sea_uri


PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?sea_uri (COUNT(?water_uri) AS ?waters)  

WHERE {

?water_uri mon:flowsInto+ ?sea_uri . ?sea_uri a mon:Sea .
?water_uri a mon:Lake .
  

}
GROUP BY ?sea_uri 
ORDER BY DESC(?waters)


----

## ex: collegamento via acqua

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?city_1_name ?city_2_name  

WHERE {

?city_uri_1 a mon:City . ?city_uri_1 mon:locatedAt* ?located_uri .
?city_uri_1 mon:name ?city_1_name .  

?located_uri mon:flowsInto+ ?water_uri . # collegamento via acqua
  
?city_uri_2 a mon:City . ?city_uri_2 mon:locatedAt* ?water_uri .
?city_uri_2 mon:name ?city_2_name .  

}

ORDER BY ?city_1_name ?city_2_name 


----

ex: città collegate tramite fiumi

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?city_1_name ?city_2_name  

WHERE {

?city_uri_1 a mon:City . ?city_uri_1 mon:locatedAt* ?located_uri .
?city_uri_1 mon:name ?city_1_name .  

?located_uri mon:flowsInto+ ?water_uri . # collegamento via acqua
?water_uri a mon:River .
  
?city_uri_2 a mon:City . ?city_uri_2 mon:locatedAt* ?water_uri .
?city_uri_2 mon:name ?city_2_name .  

}

ORDER BY ?city_1_name ?city_2_name 

----

ex: città più collegabili via acqua 

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT ?city_1_name ?city_2_name (COUNT(?water_uri) AS ?waters)

WHERE {

?city_uri_1 a mon:City . ?city_uri_1 mon:locatedAt* ?located_uri .
?city_uri_1 mon:name ?city_1_name .  

?located_uri mon:flowsInto+ ?water_uri . # collegamento via acqua
?water_uri a mon:River .
  
?city_uri_2 a mon:City . ?city_uri_2 mon:locatedAt* ?water_uri .
?city_uri_2 mon:name ?city_2_name .  

}

GROUP BY ?city_1_name ?city_2_name 
ORDER BY DESC(?waters) ?city_1_name ?city_2_name 


----

## ex: densità di popolazione vicino ai fiumi 

PREFIX mon: <http://www.semwebtech.org/mondial/10/meta#>

SELECT DISTINCT 
	?river_name 
	(COUNT(?city_population) AS ?cities) 
	(SUM(?city_population) AS ?population) 
	(SUM(?city_population) / xsd:double(COUNT(?city_population)) AS ?density)
	?country_name

WHERE {

?city_uri_1 a mon:City . ?city_uri_1 mon:locatedAt* ?located_uri .
?city_uri_1 mon:name ?city_1_name .  
?city_uri_1 mon:population ?city_population .
  
?located_uri mon:flowsInto+ ?water_uri . # collegamento via acqua
?water_uri a mon:River .
?water_uri mon:name ?river_name .
?water_uri mon:locatedIn ?country_uri . ?country_uri a mon:Country . ?country_uri mon:name ?country_name .
 
}
GROUP BY ?river_name ?country_name
ORDER BY DESC(?density) 
















