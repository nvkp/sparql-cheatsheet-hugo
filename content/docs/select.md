---
title: SELECT
weight: 1
---

## PREFIX

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?craigEmail
WHERE {
	ab:craig ab:email ?craigEmail
}
```

## LIMIT

```sparql
SELECT ?s ?p ?o WHERE {
	?s ?p ?o
} LIMIT 10
```

## Multiple Constraints

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last WHERE {
	?person ab:homeTel "(229) 276-5135" .
	?person ab:firstName ?first .
	?person ab:lastName ?last .
}
```

## Using ;

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last WHERE {
	?person ab:homeTel "(229) 276-5135" ;
		ab:firstName ?first ;
		ab:lastName ?last ;
		ab:email ?email .
}
```

## OPTIONAL

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last ?workTel ?email WHERE {
	?person ab:firstName ?first ;
		ab:lastName ?last .
	OPTIONAL {
		?person ab:workTel ?workTel ;
			ab:email ?email .
	}
}
```

## NOT EXISTS

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last WHERE {
	?person ab:firstName ?first ;
		ab:lastName ?last .
	NOT EXISTS {
		?person ab:workTel ?workNum .
	}
}
```

## FILTER

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last WHERE {
	?person ab:firstName ?first ;
		ab:lastName ?last .
	OPTIONAL {
		?person ab:workTel ?workNum .
	}
	FILTER (!bound(?workNum))
}
```

## MINUS (Subtraction)

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?first ?last WHERE {
	?person ab:firstName ?first ;
		ab:lastName ?last .
	MINUS {
		?person ab:workTel ?workNum .
	}
}
```

## DISTINCT

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT DISTINCT ?first ?last WHERE {
	?s ab:takingCourse ?class ;
           ab:firstName ?first ;
           ab:lastName ?last .		
}
```

## UNION

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT * WHERE {
	{ ?person ab:firstName ?first ; ab:lastName ?last .}
	UNION
	{ ?course ab:courseTitle ?courseName .}		
}
```

## OFFSET 

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT ?mealName WHERE {
	?s e:description ?mealName .
} 
OFFSET 2 
LIMIT 10
```

## ORDER BY

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT ?description ?date ?amount WHERE {
	?meal e:description ?description ;
	      e:date ?date ;
	      e:amount ?amount .
}

ORDER BY DESC(?amount)
```

## MAX & MIN

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT (MAX(?amount) as ?maxAmount) WHERE {
	?meal e:amount ?amount .
}
```

## COUNT

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT (COUNT(?meal) as ?mealCount)  WHERE {
	?meal e:description ?description ;
	      e:date ?date ;
	      e:amount ?amount .
}
```

## SUM

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT (SUM(?amount) as ?amountSum)  WHERE {
	?meal e:description ?description ;
	      e:date ?date ;
	      e:amount ?amount .
}
```

## AVG

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT (AVG(?amount) as ?amountAvg)  WHERE {
	?meal e:description ?description ;
	      e:date ?date ;
	      e:amount ?amount .
}
```

## GROUP BY && HAVING

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT (SUM(?amount) as ?amountSum)  WHERE {
	?meal e:description ?description ;
	      e:date ?date ;
	      e:amount ?amount .
}
GROUP BY ?description
HAVING (SUM(?amount) > 45)
```

## Subqueries

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?lastName ?courseName WHERE {
	{
		SELECT ?lastName WHERE {
			?student ab:lastName ?lastName ;
			         ab:takingCourse ?course .
		}
	}
	{
		SELECT ?courseName WHERE {
			?course ab:courseTitle ?courseName .
		}
	}

}
```

## Assigning Variables && String functions

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT ?mealCode ?amount WHERE {
	{
		# USACE -> upper case ; SUBSTR -> substring indexing from 1
		SELECT ?meal (UCASE(SUBSTR(?description, 1, 3)) as ?mealCode) WHERE { 
			?meal e:description ?description .
		}
	}
	{
		SELECT ?meal ?amount WHERE {
			?meal e:amount ?amount .
		}
	}
}
```

```sparql
PREFIX e: <http://learningsparql.com/ns/expenses#>

SELECT ?mealCode ?amount WHERE {
	?meal e:description ?description ;
	      e:amount ?amount .
	BIND(UCASE(SUBSTR(?description, 1, 3)) as ?mealCode)    
}
```

## Querying remote datasets

```sparql
PREFIX ab: <http://learningsparql.com/ns/addressbook#>

SELECT ?firstName ?lastName ?streetAddress ?city ?region ?postalCode
FROM <http://learningsparql.com/2ndeditionexamples/ex041.ttl>
WHERE {
	?s ab:firstName ?firstName ;
	   ab:lastName ?lastName ;
	   ab:address ?address .
	?address ab:postalCode ?postalCode ;
	         ab:city ?city ;
	         ab:streetAddress ?streetAddress ;
	         ab:region ?region .   
}
```

## Federated Queries (Remote Endpoint)

```sparql
SELECT ?p ?o
WHERE {
	SERVICE <http://DBpedia.org/sparql> {
		SELECT ?p ?o
		WHERE {
			<http://dbpedia.org/resource/Joseph_Hocking> ?p ?o .
		}
	}
}
LIMIT 10
```

## GRAPH

```sparql
SELECT ?s ?p ?o ?g WHERE {
	GRAPH ?g {
		?s ?p ?o .
	}
}
LIMIT 10
```