
# Menu Designer

## Table of Contents

1. [Project Overview](#project-overview)
2. [Why This Project Matters](#why-this-project-matters)
3. [Technologies Used](#technologies-used)
4. [Why These Technologies Were Chosen](#why-these-technologies-were-chosen)
5. [System Workflow](#system-workflow)
6. [Why This Process Was Used](#why-this-process-was-used)
7. [Outputs and Evaluation](#outputs-and-evaluation)
8. [Conclusion](#conclusion)

---

## Project Overview

The **Menu Designer** project is a retrieval-augmented generation (RAG) system built to generate menu recommendations based on user needs and preferences. Instead of relying only on a language model to produce answers from memory, the system first retrieves relevant recipe or menu information from a recipe collection and then uses that retrieved content to generate a more grounded and relevant response.

The goal of the project is to create a system that can recommend menus in a way that is more accurate, more explainable, and more aligned with user constraints such as food preferences or dietary restrictions.

---

## Why This Project Matters

A menu recommendation task is not just a text generation problem. It also requires the system to:

* find relevant recipes,
* understand the user query,
* respect dietary constraints,
* and generate a coherent final response.

A standard language model may produce fluent text, but it can still hallucinate or ignore important constraints. By using a RAG pipeline, the project improves reliability because the final answer is grounded in retrieved items from the recipe dataset.

This makes the system more suitable for practical recommendation tasks where relevance and constraint satisfaction matter more than creative generation alone.

---

## Technologies Used

This project uses the following core technologies:

* **RAG (Retrieval-Augmented Generation)** as the overall framework
* **Dense retrieval** for semantic search
* **FAISS** for efficient similarity search over recipe representations
* **BGE-small embeddings** to convert queries and recipes into dense vector representations
* **Post-retrieval filtering** to remove items that violate user constraints, such as dairy-free requirements
* **Query rewriting** for cases where the original user request is too vague
* **LLM-based generation** to produce the final menu recommendation
* **LLM-as-a-judge evaluation** to assess the quality of generated outputs

---

## Why These Technologies Were Chosen

### RAG

RAG was chosen because the task requires both retrieval and generation. The system needs to find relevant recipes first, then generate a helpful answer using those retrieved results. This improves factual grounding and reduces the chance of unsupported recommendations.

### Dense Retrieval

Dense retrieval was selected because menu and recipe queries are often semantic rather than exact keyword matches. Users may describe a meal in a natural way, and embedding-based retrieval is better at capturing meaning beyond shared words.

### FAISS

FAISS was used because it allows fast and scalable similarity search over dense vectors. This makes retrieval efficient even when working with a larger recipe collection.

### BGE-small Embeddings

BGE-small was chosen as the embedding model because it provides compact semantic representations that work well for matching user queries to recipe content. It offers a strong balance between retrieval quality and efficiency.

### Post-Retrieval Filtering

Filtering was added after retrieval to make sure the final candidates satisfy hard constraints. For example, if the user requests a dairy-free menu, recipes containing dairy should be excluded even if they are semantically similar to the query.

### Query Rewriting

Query rewriting was explored because some user requests can be too short, vague, or underspecified. Rewriting helps turn these into more retrieval-friendly queries, which can improve the relevance of retrieved results.

### LLM-as-a-Judge

Evaluation in generative systems is difficult because there may not be a single correct answer. LLM-based judging was used to assess helpfulness, relevance, and constraint satisfaction in a more flexible way than exact-match metrics.

---

## System Workflow

The Menu Designer follows a multi-step pipeline:

### 1. User Query Input

The system receives a user request describing the desired menu or meal preferences.

### 2. Query Processing

If the query is vague or incomplete, it may be rewritten into a clearer form to improve retrieval performance.

### 3. Dense Retrieval

The processed query is embedded and compared against recipe embeddings using FAISS to retrieve the most relevant candidates.

### 4. Constraint-Based Filtering

Retrieved recipes are filtered to remove results that do not satisfy user requirements, such as dietary restrictions.

### 5. Final Context Selection

The remaining relevant recipes are used as the context for generation.

### 6. Response Generation

A language model uses the retrieved context to generate the final menu recommendation.

### 7. Evaluation

Generated outputs are assessed using an LLM-as-a-judge setup to measure quality, relevance, and whether the recommendations satisfy the intended constraints.

---

## Why This Process Was Used

This process was designed to separate the problem into smaller, more reliable stages.

* **Retrieval first** ensures the system works from relevant recipe evidence instead of generating unsupported suggestions.
* **Filtering after retrieval** ensures that hard user constraints are enforced directly.
* **Generation last** allows the model to present results in a natural and helpful way.
* **Evaluation with a judge model** provides a more realistic assessment for open-ended recommendations.

This pipeline is especially useful for recommendation tasks because it combines structure with flexibility. The retrieval stage improves grounding, the filtering stage improves safety and constraint satisfaction, and the generation stage improves readability and usefulness.

---

## Outputs and Evaluation

The main output of the system is a generated menu recommendation based on the user’s request and the retrieved recipe context.

The project also evaluates output quality using an LLM-as-a-judge approach. This is helpful because traditional evaluation metrics are often limited for creative or open-ended recommendation tasks. The judging process focuses more on whether the final answer is relevant, sensible, and aligned with the user’s requirements.

---

## Conclusion

The Menu Designer project demonstrates how a RAG-based system can be used for intelligent menu recommendation. Rather than treating the problem as pure text generation, the project combines semantic retrieval, filtering, and generation to produce answers that are more grounded and practically useful.

The selected technologies were chosen to support accuracy, efficiency, and constraint handling. Overall, this design makes the system more reliable for real-world recommendation scenarios where relevance and user needs are critical.
