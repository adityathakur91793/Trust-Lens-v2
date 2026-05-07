# Trust-Lens-v2
More advanced version of trust lens so we can eleminate LLM Hillunication more efficiently

-> Core Idea

Add an invisible validation layer on top of LLMs
~ Didn’t build new model
~ Check if answer is reliable using consistency + evidence

-> 1. OLD PIPELINE (My initial idea)

User Question
  ->
Generate 3 similar questions (Q1, Q2, Q3)
  ->
Get answers (A1, A2, A3)
  ->
Cosine Similarity
  ->
Factor / Probability Check
  ->
Final Answer + Accuracy %

-> 2. PROBLEMS IN OLD PIPELINE

Problem 1: “Collective hallucination”

All answers wrong but similar
 → high similarity → false confidence 

Problem 2: Low diversity
Q1, Q2, Q3 almost same
 → same answers → fake validation 

Problem 3: Model bias
Same LLM or similar models
 → same mistakes repeated 

Problem 4: No grounding
No external truth check
 → system is self-referential

Problem 5: Weak scoring
“factor / probability” not defined
 → not scientific → paper rejected

-> 3. FIXES 

FIX 1: Evidence Layer (MOST IMPORTANT)
Add:
Answer → Claim Extraction → Evidence Retrieval → Verification
Extract facts
Search Wikipedia
Compare using embeddings
~ Converts system from guessing → verifying

FIX 2: Enforced Question Diversity
Rule:
similarity(Q1, Q2) < 0.85
similarity(Q1, Q3) < 0.85
~ ensures different reasoning paths

FIX 3: Multi-Model Setup
Use:
OpenAI
Google
Anthropic
vary:
prompts
~ reduces shared bias

FIX 4: Proper Scoring Function
Replace vague “factor” with:
Confidence =
 w1 * Answer Similarity
+ w2 * Question Diversity
+ w3 * Cross-Model Agreement
+ w4 * Evidence Support
~ now measurable + publishable

4. FINAL PIPELINE (TRUSTLENS v2 — STRONG)
User Question
 -> 
Question Expansion
-- Q1, Q2, Q3 
-- Diversity Check (SBERT)
 -> 
Multi-LLM Layer
-- Model A
-- Model B
-- Model C
 -> 
Answer Pool
-- A1, A2, A3...
 -> 
Processing
-- Normalize
-- Claim Extraction
 -> 
Validation Layer
-- Answer Similarity
-- Cross-Model Agreement
-- Evidence Verification 
 -> 
Scoring Engine
 -> 
Final Output:
- Answer
- Confidence %
- Hallucination flag

-> 5. TECH STACK
NLP / Embeddings
Sentence-BERT
Retrieval
FAISS
NLP Processing
spaCy
LLM APIs
-OpenAI
-Google
-Anthropic

-> 6. LIMITATIONS (write honestly)
If evidence source wrong → system fails
Cost increases (multiple APIs)
Latency High
Complex questions still hard

# Currently working on Working Prototype of Trust-Lens-v2 and Also Trying to elemnate Limatations in V3
