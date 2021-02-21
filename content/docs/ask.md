---
title: ASK
weight: 5
---

Returns Yes or No depending on whether the query has a solution.

```sparql
PREFIX dbpedia: <http://dbpedia.org/resource/>
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
PREFIX mo: <http://purl.org/ontology/mo/>

ASK
WHERE { dbpedia:The_Beatles mo:member dbpedia:Paul_McCartney }
```