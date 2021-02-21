---
title: CONSTRUCT
weight: 2
--- 

Creates a new RDF graph.

```sparql
CONSTRUCT { ?person vcard:fn ?fullName } WHERE {
	?person vcard:given-name ?givenName .
	?person vcard:family-name ?familyName .
	BIND(concat(?givenName, " ", ?familyName) as ?fullName)
}
```