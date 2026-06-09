---
layout: default
title: LLM Prompts & Triples
---
<div style="text-align: center; margin-bottom: 30px;">
  <a href="index.html" class="btn" style="margin: 5px; padding: 10px 15px;">🏠 Home</a>
  <a href="topic.html" class="btn" style="margin: 5px; padding: 10px 15px;">🌸 Topic & Gap</a>
  <a href="sparql.html" class="btn" style="margin: 5px; padding: 10px 15px;">📊 SPARQL Queries</a>
  <a href="prompts.html" class="btn" style="margin: 5px; padding: 10px 15px;">🤖 LLM Prompts</a>
  <a href="challenges.html" class="btn" style="margin: 5px; padding: 10px 15px;">🛠️ Challenges</a>
</div>
# LLM Prompting & Knowledge Generation

---

### 🔬 Our Methodological Choice: Variable Isolation
Unlike alternative projects that change the target question for every single prompting technique, our team made a deliberate, scientifically sound choice. We kept the **exact same complex informational goal constant** across all our experiments: extracting the 9 mythological characters from Botticelli's *Primavera* and capturing their Neoplatonic allegories. 

By isolating the target variable, we were able to strictly evaluate how changing only the *prompt structure* impacts the output quality and the syntactic correctness of the generated RDF Turtle code.

---

### 1️⃣ Zero-Shot Prompting: Testing Raw Capabilities
We asked both models to generate the triples directly, relying purely on their pre-trained knowledge without giving them any prior structural examples or formatting guidelines.

* **The Prompt:** *“Act as a knowledge engineer. Analyze Botticelli's 'La Primavera' (ArCo IRI: <https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550>). Extract all the mythological characters and map them using the ArCo property `a-cd:hasSubject`. Output the result in Turtle syntax.”*
* **Observations:** Both models identified the main characters due to their broad historical training data, but the code output was highly inconsistent. They completely forgot language tags, mixed namespaces, and failed to generate rich descriptive comments.

---

### 2️⃣ Few-Shot Prompting: Scaffolding via Examples
To enforce structural and ontological alignment, we provided the models with a concrete template example showing exactly how a clean ArCo instance should look using `rdfs:comment` and the `@it` language tag.

* **The Prompt:** *(We pasted an example template of a correctly formatted Turtle triple before asking our main question)*.
* **The Result:** A major leap in semantic quality. Both models strictly mirrored our template layout. Below is the clean, verified Turtle file generated during this step, which we can officially use to enrich the ArCo repository:

```turtle
@prefix ex: [http://example.org/](http://example.org/) .
@prefix rdfs: [http://www.w3.org/2000/01/rdf-schema#](http://www.w3.org/2000/01/rdf-schema#) .
@prefix a-cd: [https://w3id.org/arco/ontology/context-description/](https://w3id.org/arco/ontology/context-description/) .

[https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550](https://w3id.org/arco/resource/HistoricOrArtisticProperty/0900158550) 
    a-cd:hasSubject ex:Venere, ex:Mercurio, ex:Cupido, ex:Flora, ex:Clori, ex:Zefiro .

ex:Venere a a-cd:Subject ;
    rdfs:label "Venere"@it ;
    rdfs:comment "Figura centrale del dipinto, rappresenta la Venus Humanitas, simbolo di equilibrio neoplatonico, armonia e mediazione tra l'amore terreno e quello spirituale."@it .

ex:Mercurio a a-cd:Subject ;
    rdfs:label "Mercurio"@it ;
    rdfs:comment "Posto all'estrema sinistra, allontana le nubi del mondo sensibile con il caduceo. Simboleggia la ragione e il ritorno dell'anima alla contemplazione celeste."@it .
3️⃣ Chain-of-Thought (CoT) Prompting & The "Instruction Failure"
We pushed the models to use multi-stage reasoning by forcing them to follow three mandatory analytical steps: scan the painting spatially from right to left, write down the philosophical/theological allegory, and only then compile the Turtle graph.
🟢 ChatGPT Performance (Success)
ChatGPT followed the CoT layout flawlessly. It analyzed the painting right-to-left (starting with Zephyrus and ending with Mercury), providing an outstanding Neoplatonic analysis citing Marsilio Ficino and the Medici court. It then generated pristine Turtle triples perfectly aligned with the graph schema.
🔴 Gemini Performance (Vicious Failure ❌)
Gemini completely broke down under this structural constraint. Instead of following the instructions, it explicitly responded with a hard refusal:
"Non posso fornire il mio ragionamento interno dettagliato o la catena di pensiero passo per passo. Posso però fornire una sintesi del procedimento e il risultato dell’analisi."
The Breakdown: Not only did Gemini openly refuse to execute the Chain-of-Thought reasoning steps, but it also completely forgot to output the required Turtle RDF code block, providing only a surface-level textual summary of the scene. This highlighted a major issue with model-specific guardrails and prompt compliance under rigid constraints.
🧭 Navigation
<a href="sparql.html" class="btn">Back to SPARQL Queries</a>
<a href="challenges.html" class="btn">Proceed to Step 5: Challenges & Conclusion</a>
