---
layout: default
title: Challenges & Conclusion
---
<div style="text-align: center; margin-bottom: 30px;">
  <a href="index.html" class="btn" style="margin: 5px; padding: 10px 15px;">🏠 Home</a>
  <a href="topic.html" class="btn" style="margin: 5px; padding: 10px 15px;">🌸 Topic & Gap</a>
  <a href="sparql.html" class="btn" style="margin: 5px; padding: 10px 15px;">📊 SPARQL Queries</a>
  <a href="prompts.html" class="btn" style="margin: 5px; padding: 10px 15px;">🤖 LLM Prompts</a>
  <a href="challenges.html" class="btn" style="margin: 5px; padding: 10px 15px;">🛠️ Challenges</a>
</div>
# Faced Challenges & Final Conclusions


---

### 🛠️ Technical Challenges Faced During the Project
Our team encountered several technical and conceptual hurdles throughout this knowledge engineering lifecycle. Here is how we addressed them:

1. **SPARQL Syntax Rigidity:** Crafting an exploratory query that logically integrated all 7 required modifiers without generating massive redundant arrays or timing out.
   * *Our Solution:* We developed a step-by-step query progression (Tappe A, B, C) that gradually refined the scope of data, converting initial noise into a highly clean, actionable output.
2. **LLM Syntactic Drift & Laziness:** During the Zero-Shot and Chain-of-Thought tests, the language models frequently drifted away from standard ArCo schemas, hallucinated predicates, or omitted code blocks entirely (as seen with Gemini's stubborn refusal).
   * *Our Solution:* We solved this by implementing strict role-prompting (forcing the LLM to act as a *Knowledge Engineer*) and deploying rigorous Few-Shot templates to strictly constrain the vocabulary and the output syntax.
3. **Institutional Endpoint Instability:** On multiple occasions, the public ArCo SPARQL endpoint experienced severe lag or temporary downtimes, stalling our live verification phases.
   * *Our Solution:* We cached query templates locally and ran asynchronous data exploration sessions to maximize efficiency.

---

### 🎓 Final Takeaways & Conclusions
* **The Power of Hybrid Systems:** While Knowledge Graphs are unbeatable for deterministic data structure and truth tracking, LLMs are immensely powerful tools to unlock hidden contextual narratives (such as philosophical allegories) that traditional human cataloging leaves blank.
* **The Prompt Engineering Impact:** Keeping our informational goal perfectly constant proved that prompt engineering is a legitimate science. A simple change in structure (Few-Shot vs Zero-Shot) can mean the difference between syntax errors and pristine, graph-ready RDF Turtle triples.
* **The Crucial Need for Human Oversight:** Gemini's open refusal to compile code under CoT constraints proves that AI cannot yet be fully automated in knowledge pipelines. The "Human-in-the-Loop" remains the ultimate gold standard for checking syntax, validating truth, and maintaining graph integrity.

---

### 🧭 Navigation
<a href="prompts.html" class="btn">Back to LLM Prompts & RDF</a>
<a href="index.html" class="btn">Return to Home Page</a>
