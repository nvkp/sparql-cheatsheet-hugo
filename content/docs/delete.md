---
title: DELETE
weight: 4
---

## DELETE DATA

```sparql
PREFIX ns: <https://example.org/ns#>

DELETE DATA
{
	GRAPH <https://example/bookStore> {
		<https://example/book1> dct:title "Fundamentals of Compiler Desing"@en .
	}
}
```

## DELETE

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1>

DELETE { ?person ?property ?value }
WHERE {
	?person ?property ?value ;
		foaf:givenName "Fred"@en .
}
```

```sparql
DELETE { GRAPH <g1> { a b c }}
INSERT { GRAPH <g1> { x y z }}
USING <g1>
WHERE { ... }
```

## DELETE WHERE

```sparql
DELETE WHERE {
	?person foaf:givenName "Fred"@en ;
		?property ?value .
}
```