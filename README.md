# Agentic RAG Application

An advanced Retrieval-Augmented Generation (RAG) application powered by autonomous agents. Unlike traditional RAG pipelines that follow a strict linear sequence, this project implements an **Agentic loop** capable of query routing, iterative self-correction, document grading, and fallback web-searching.

---

## 🚀 Key Features

* **Intelligent Query Routing:** Dynamically decides whether to query local vector stores, look up external APIs, or fall back to web search.
* **Self-Correction Loop:** Evaluates retrieved documents for relevance and filters out noise before generation.
* **Hallucination Grader:** Validates the final LLM response against the source documents to ensure grounding and prevent hallucinations.
* **Stateful Memory:** Maintains conversational context across multi-turn reasoning steps.

## 🛠️ Architecture

```text
               +------------------+
               |  User Question   |
               +--------+---------+
                        |
                        v
               +------------------+
               |   Router Agent   |
               +---+----------+---+
                   |          |
      [Local Vector DB]    [Web Search API]
                   |          |
                   v          v
         +--------------------------+
         | Document Relevance Check |
         +--------------+-----------+
                        |
            [Relevant]  |  [Not Relevant] -> (Rewrite Query Loop)
                        v
         +--------------------------+
         |     Generate Response    |
         +--------------+-----------+
                        |
                        v
         +--------------------------+
         |   Hallucination Grader   |
         +--------------------------+
