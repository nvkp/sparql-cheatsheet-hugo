---
title: DESCRIBE
weight: 6
---

Returns the RDF graph data about a resource.

```sparql
PREFIX foaf:  <http://xmlns.com/foaf/0.1/>
DESCRIBE ?ford WHERE {
  ?ford foaf:name "FORD MOTOR CO" .
}
```