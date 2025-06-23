# SQuAI: Scientific Question-Answering with Multi-Agent Retrieval-Augmented Generation

SQuAI is a scalable and trustworthy **multi-agent Retrieval-Augmented Generation (RAG)** system for scientific question answering (QA). It is designed to address the challenges of answering complex, open-domain scientific queries with high relevance, verifiability, and transparency. This project is introduced in our CIKM 2025 demo paper:  
**"SQuAI: Scientific Question-Answering with Multi-Agent Retrieval-Augmented Generation"**  
Link to: [Demo Video](https://www.youtube.com/watch?v=aGDrtsiZDQA&feature=youtu.be)
---

## Key Features

- **Multi-agent architecture** for decomposing and answering complex questions
- **Hybrid retrieval system** (sparse + dense) optimized for scientific literature
- **In-line citations** and **citation context** for transparent and verifiable answers
- **User interface** for configurable, interactive QA with support for multiple retrieval/generation settings
- Supports over **2.3 million full-text arXiv papers** via the [unarXive 2024](https://huggingface.co/datasets/ines-besrour/unarxive_2024) dataset
- Comes with a **benchmark of 1,000 QA-evidence pairs** for evaluation
---

## System Architecture

SQuAI consists of four key agents working collaboratively to deliver accurate, faithful, and verifiable answers:

1. **Agent 1: Decomposer**  
   Decomposes complex user queries into simpler, semantically distinct sub-questions. This step ensures that each aspect of the question is treated with focused retrieval and generation, enabling precise evidence aggregation.

2. **Agent 2: Generator**  
   For each sub-question, this agent processes retrieved documents to generate structured **Question–Answer–Evidence (Q-A-E)** triplets. These triplets form the backbone of transparent and evidence-grounded answers.

3. **Agent 3: Judge**  
   Evaluates the relevance and quality of each Q-A-E triplet using a learned scoring mechanism. It filters out weak or irrelevant documents based on confidence thresholds, dynamically tuned to the difficulty of each query.

4. **Agent 4: Answer Generator**  
   Synthesizes a final, coherent answer from filtered Q-A-E triplets. Critically, it includes **fine-grained in-line citations** and citation context to enhance trust and verifiability. Every factual statement is explicitly linked to one or more supporting documents.

###  Retrieval Engine

The agents are supported by a **hybrid retrieval system** that combines:
- **Sparse retrieval** (BM25) for keyword overlap and exact matching.
- **Dense retrieval** (E5 embeddings) for semantic similarity.

The system interpolates scores from both methods to maximize both lexical precision and semantic coverage.

```math
S_{hybrid}(d) = \alpha \cdot S_{sparse}(d) + (1 - \alpha) \cdot S_{dense}(d)
```
\(\alpha = 0.65\), based on empirical tuning. This slightly favors dense retrieval while retaining complementary signals from sparse methods, ensuring both semantic relevance and precision.

---

## 🖥️ User Interface

SQuAI includes an interactive web-based UI built with **Streamlit** and backed by a **FastAPI** server. Key features include:

- A simple input form for entering scientific questions.
- Visualization of decomposed sub-questions.
- Toggle between sparse, dense, and hybrid retrieval modes.
- Adjustable settings for document filtering thresholds and top-k retrieval.
- Display of generated answers with **fine-grained in-line citations**.
- Clickable references linking to original arXiv papers.

---

## Benchmarks & Evaluation

We evaluate SQuAI using three QA datasets designed to test performance across varying complexity levels:

- **LitSearch**: Real-world literature review queries from computer science.
- **unarXive Simple**: General questions with minimal complexity.
- **unarXive Expert**: Highly specific and technical questions requiring deep evidence grounding.

Evaluation metrics (via [DeepEval](https://deepeval.com)) include:

- **Answer Relevance** – How well the answer semantically matches the question.
- **Contextual Relevance** – How well the answer integrates retrieved evidence.
- **Faithfulness** – Whether the answer is supported by cited sources.

SQuAI improves combined scores by up to **12%** in faithfulness compared to a strong RAG baseline.

---

## Dataset & Resources

- **unarXive 2024**: Full-text arXiv papers with structured metadata, section segmentation, and citation annotations. [Hugging Face Dataset](https://huggingface.co/datasets/ines-besrour/unarxive_2024)
- **QA Triplet Benchmark**: 1,000 synthetic question–answer–evidence triplets for reproducible evaluation.
---

## Conclusion

SQuAI demonstrates how collaborative agents, hybrid retrieval, and verifiable citation generation can significantly enhance trust and accuracy in scientific question answering. Its architecture is modular, transparent, and scalable—making it suitable for both research and real-world applications across disciplines.

---


