---
title: INSERT
weight: 3
---

Adds triples to a graph.

## INSERT DATA

```sparql
PREFIX ns: <https://example.org/ns#>

INSERT DATA
{
	GRAPH <https://example/bookStore> {
		<https://example/book1> ns:price 42 .
	}
}
```

## INSERT

```sparql
PREFIX foaf: <http://xmlns.com/foaf/0.1>
PREFIX eg: <http://example.org/ns#>

INSERT { ?person eg:something eg:someone }
WHERE {
	?person ?property ?value ;
		foaf:givenName "Fred"@en .
}
```