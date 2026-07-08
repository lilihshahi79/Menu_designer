Yup — here’s an updated README version with those sections added in naturally.

# Menu Designer

## Table of Contents

1. [Project Overview](#project-overview)
2. [How the Project Came About](#how-the-project-came-about)
3. [The Motivation](#the-motivation)
4. [What Problem It Hopes to Solve](#what-problem-it-hopes-to-solve)
5. [The Intended Use](#the-intended-use)
6. [Technologies Used](#technologies-used)
7. [Why These Technologies Were Chosen](#why-these-technologies-were-chosen)
8. [System Workflow](#system-workflow)
9. [Why This Process Was Used](#why-this-process-was-used)
10. [Challenges](#challenges)
11. [Limitations](#limitations)
12. [Outputs and Evaluation](#outputs-and-evaluation)
13. [Conclusion](#conclusion)

---

## Project Overview

**Menu Designer** is a Retrieval-Augmented Generation (RAG) project built to generate menu recommendations based on a user’s preferences, goals, and dietary constraints. Instead of relying only on a language model to answer from its internal knowledge, the system first retrieves relevant recipes from a dataset and then uses those retrieved results to generate a more grounded and useful recommendation.

The project is designed to make menu generation more reliable, more relevant, and more aligned with what the user actually asks for.

---

## How the Project Came About

This project came out of the idea that menu recommendation is not only a text generation task, but also a retrieval and reasoning task. A useful menu suggestion needs more than fluent language. It needs to reflect user requirements, retrieve relevant meal options, and combine them into a sensible final response.

Rather than building a system that simply generates food suggestions from memory, this project explores how combining retrieval with generation can produce recommendations that are better grounded in actual recipe data.

---

## The Motivation

The motivation behind this project is to improve the quality of menu recommendations by making them more evidence-based. In many recommendation or generation tasks, a model may produce text that sounds convincing but does not fully match the user’s needs.

For food-related recommendations, that becomes a real issue because users may care about things like dietary restrictions, ingredients, or meal type. This project is motivated by the need for a system that can understand user requests better and produce responses that are not just fluent, but also relevant and practical.

---

## What Problem It Hopes to Solve

The main problem this project aims to solve is the gap between natural-sounding generation and actually useful recommendation. A standard language model might generate a menu that sounds reasonable, but it may ignore constraints, invent unsuitable meals, or fail to retrieve the most relevant options.

This project tries to solve that by grounding generation in retrieved recipe data. That way, the final menu is supported by relevant examples instead of being produced only from model memory.

---

## The Intended Use

The intended use of the Menu Designer is to support users who want menu suggestions tailored to their preferences or dietary needs. It is designed for scenarios where the user may want a menu based on constraints such as being dairy-free, looking for a certain meal type, or wanting a specific style of dish.

The system is intended as a recommendation assistant rather than a fully autonomous planner. Its purpose is to provide relevant and grounded menu ideas that users can review and adapt.

---

## Technologies Used

This project uses the following main technologies:

* **Retrieval-Augmented Generation (RAG)** as the overall framework
* **Dense retrieval** for semantic matching
* **FAISS** for efficient vector similarity search
* **BGE-small embeddings** for converting recipes and queries into dense representations
* **Post-retrieval filtering** to enforce dietary constraints
* **Query rewriting** for vague or underspecified queries
* **Large Language Model generation** for the final response
* **LLM-as-a-judge evaluation** for assessing output quality

---

## Why These Technologies Were Chosen

### RAG

RAG was selected because the task needs both retrieval and generation. The system must first find relevant recipes and then generate a response using those recipes as support.

### Dense Retrieval

Dense retrieval was chosen because recipe and menu requests are often semantic. Users may describe what they want in natural language, and dense embeddings capture meaning better than simple keyword overlap.

### FAISS

FAISS was used because it allows fast similarity search over dense vectors, which makes retrieval efficient and scalable.

### BGE-small Embeddings

BGE-small was chosen because it provides compact semantic representations with a good balance between effectiveness and efficiency.

### Post-Retrieval Filtering

Filtering was added to enforce hard constraints after retrieval. This is important because semantically relevant recipes may still violate dietary requirements.

### Query Rewriting

Query rewriting helps when user input is too broad or vague. A clearer query improves the quality of the retrieved candidates.

### LLM-as-a-Judge

Since menu generation is open-ended, there is not always one exact correct answer. LLM-based judging provides a more flexible way to evaluate relevance, usefulness, and constraint satisfaction.

---

## System Workflow

The system follows a step-by-step pipeline:

### 1. User Query Input

The system receives a user request describing menu preferences or dietary needs.

### 2. Query Processing

If the original query is vague, it may be rewritten into a clearer and more retrieval-friendly form.

### 3. Dense Retrieval

The processed query is embedded and matched against recipe embeddings using FAISS to retrieve relevant candidates.

### 4. Constraint-Based Filtering

Retrieved recipes are filtered to remove any results that do not satisfy user constraints.

### 5. Final Context Selection

The remaining retrieved recipes are selected as the evidence base for generation.

### 6. Response Generation

A language model uses the retrieved context to generate the final menu recommendation.

### 7. Evaluation

The generated outputs are assessed with an LLM-as-a-judge framework to measure quality and relevance.

---

## Why This Process Was Used

This process was used because it breaks the task into smaller, more reliable stages. Retrieval helps ground the response in actual recipe data. Filtering makes sure hard constraints are respected. Generation then turns the retrieved information into a readable and useful final answer.

This pipeline was chosen because it offers a stronger balance between relevance, flexibility, and control than using a generator alone.

---

## Challenges

One challenge in this project is that a retrieved recipe may be semantically relevant while still violating a user constraint. That means retrieval alone is not enough, and extra filtering is necessary.

Another challenge is handling vague user queries. If the query is not specific enough, retrieval quality can drop. There is also the challenge of evaluating generated recommendations, since open-ended tasks do not always have one single correct answer.

A further challenge is balancing retrieval quality with computational efficiency, especially when experimenting with different retrievers, filters, or query reformulation strategies.

---

## Limitations

This project has some limitations. First, the system depends on the quality and coverage of the recipe dataset. If the relevant recipes are not present, the final answer will still be limited.

Second, retrieval quality is not perfect. Even dense retrieval can return items that are only partially relevant. Third, post-retrieval filtering may reduce the number of usable candidates, especially for strict dietary queries.

Finally, LLM-based evaluation is useful but not flawless. It can provide a practical assessment, but it is still an approximate judging method rather than a perfect measure of recommendation quality.

---

## Outputs and Evaluation

The main output of the system is a generated menu recommendation grounded in retrieved recipe evidence.

To evaluate the quality of these recommendations, the project uses an LLM-as-a-judge setup. This evaluation focuses on whether the output is relevant, coherent, and aligned with the user’s constraints, which is more suitable for this kind of open-ended recommendation task than exact-match metrics alone.

---

## Conclusion

The Menu Designer project demonstrates how a RAG-based pipeline can improve menu recommendation by combining retrieval, filtering, and generation. Rather than treating the task as pure text generation, the system grounds its answers in retrieved recipes and applies extra steps to better satisfy user needs.

Overall, the project aims to produce recommendations that are more practical, more relevant, and more trustworthy for real-world menu suggestion scenarios.


