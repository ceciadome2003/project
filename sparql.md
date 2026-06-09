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
Result Analysis: The endpoint returned several omonyms, duplicates, and mixed English/Italian labels. This forced us to restrict our search parameters in the next step to clean the data.


🔹 Tappa B: Author and Language Filtering
To isolate Botticelli's exact painting and clear out all the dataset noise, we added a strict regex filter on the author's name ("Botticelli") and forced the engine to only display titles explicitly tagged in Italian (⁠@it⁠).
PREFIX arco: [https://w3id.org/arco/ontology/arco/](https://w3id.org/arco/ontology/arco/)
PREFIX a-cd: [https://w3id.org/arco/ontology/context-description/](https://w3id.org/arco/ontology/context-description/)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)

SELECT DISTINCT ?artwork ?title ?authorLabel
WHERE {
    ?artwork a arco:HistoricOrArtisticProperty .
    ?artwork rdfs:label ?title .
    ?artwork a-cd:hasAuthor ?author .
    ?author rdfs:label ?authorLabel .
    
    FILTER(REGEX(?title, "primavera", "i"))
    FILTER(REGEX(?authorLabel, "botticelli", "i"))
    FILTER(lang(?title) = "it")
}
ORDER BY ?title
This query successfully isolated the unique, official IRI for Botticelli's masterpiece inside ArCo: ⁠https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550⁠.


🔹 Tappa C: Exposing the Informational Void (Definitive Query)
Now that we possessed the exact target IRI, we built our final query using an ⁠OPTIONAL⁠ block to extract all subjects associated with the painting. This query is fully compliant with the course requirements as it integrates all 7 mandatory SPARQL keywords: ⁠DISTINCT⁠, ⁠UNION⁠, ⁠OPTIONAL⁠, ⁠FILTER⁠, ⁠REGEX⁠, ⁠LIMIT⁠, and ⁠ORDER BY⁠.
PREFIX arco: [https://w3id.org/arco/ontology/arco/](https://w3id.org/arco/ontology/arco/)
PREFIX a-cd: [https://w3id.org/arco/ontology/context-description/](https://w3id.org/arco/ontology/context-description/)
PREFIX rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#)

SELECT DISTINCT ?artwork ?title ?subject
WHERE {
    { ?artwork a arco:HistoricOrArtisticProperty . }
    UNION
    { ?artwork a arco:CulturalProperty . }
    
    ?artwork rdfs:label ?title .
    
    FILTER(?artwork = [https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550](https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550))
    FILTER(lang(?title) = "it")
    
    OPTIONAL { ?artwork a-cd:hasSubject ?subject . }
}
ORDER BY ?title
LIMIT 10

🚨 Proving the Gap
Below is the official screenshot of our live query execution inside the institutional ArCo SPARQL Endpoint. As clearly demonstrated by the results table, the graph only links the painting to a single, flat generic literal value: "Allegoria della Primavera".
<img width="1600" height="684" alt="image" src="https://github.com/user-attachments/assets/8a97b399-c97a-4d63-9537-f2900c1d05a3" />

There is absolutely no trace of Venus, Mercury, Cupid, the Three Graces, or any of the rich iconographical data. The graph has a severe information gap, which our team will now solve in the next section using Prompt Engineering techniques.

🧭 Navigation
<a href="topic.html" class="btn">Back to Topic & Gap</a>
<a href="prompts.html" class="btn">Proceed to Step 4: LLM Prompts & RDF</a>
