---
layout: default
title: SPARQL Queries
---

# SPARQL Queries & Discovery of the Gap

---

### 📊 Our Incremental Query Strategy
To prove the existence of the knowledge gap in a methodologically sound way, our team did not just throw a massive query at the endpoint. We designed a **three-step incremental process** to map the dataset, filter out noise, and eventually expose the informational void regarding Botticelli's *Primavera*.

---

### 🔹 Tappa A: Broad Dataset Mapping
Our first goal was to find every cultural property containing the word "primavera" in its label. We used a `UNION` to search both fine arts and generic cultural items, and sorted them alphabetically with `ORDER BY` to inspect the results without an artificial limit.

```sparql
PREFIX arco: [https://w3id.org/arco/ontology/arco/](https://w3id.org/arco/ontology/arco/)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)

SELECT DISTINCT ?artwork ?title
WHERE {
    { ?artwork a arco:HistoricOrArtisticProperty . }
    UNION 
    { ?artwork a arco:CulturalProperty . }
    
    ?artwork rdfs:label ?title .
    FILTER(REGEX(?title, "primavera", "i"))
}
ORDER BY ?title
