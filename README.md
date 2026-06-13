# 🧠 RAG → Agentic RAG → MCP — Learning Hub

A guided learning path through retrieval, reasoning, and connectivity for modern AI systems. This file is the **root index** — start here and follow the path through each guide.

---

## 📖 Learning Path

| Stage | Guide | Focus |
|---|---|---|
| 1️⃣ | [**RAG — Zero to Hero**](files/rag-zero-to-hero.md) | Foundations of Retrieval-Augmented Generation — embeddings, chunking, vector DBs, reranking, HyDE |
| 2️⃣ | [**Agentic RAG — Zero to Hero**](files/agentic-rag-zero-to-hero.md) | Agents add planning, reflection, multi-agent coordination, memory stacks, and workflow patterns on top of RAG |
| 3️⃣ | [**MCP — Zero to Hero**](files/MCP-zero-to-hero.md) | The Model Context Protocol — Host/Client/Server architecture, Tools/Resources/Prompts, JSON-RPC, sampling, security |
| 4️⃣ | [**Relevance Graph**](files/relevance-graph.md) | Ties everything together — architecture diagrams, mindmap, comparison table, and cross-guide glossary |

```
RAG  ──(adds reasoning, planning & tool use)──▶  Agentic RAG  ──(needs standard tool/data protocol)──▶  MCP
  ▲                                                                                                       │
  └──────────────────────────(RAG pipeline lives behind an MCP server as a Resource)────────────────────┘
```

---

## 📂 Files in This Project

- `README.md` — this file (root index)
- `rag-zero-to-hero.md` — RAG fundamentals
- `agentic-rag-zero-to-hero.md` — Agentic patterns on top of RAG
- `MCP-zero-to-hero.md` — Model Context Protocol deep dive
- `relevance-graph.md` — How all three connect (diagrams + glossary)

---

## ⚡ Quick Comparison

| Dimension | RAG | Agentic RAG | MCP |
|---|---|---|---|
| Core question | Ground answers in external knowledge | Make retrieval multi-step & self-correcting | Standardize tool/data access |
| Unit of work | retrieve → augment → generate | plan → act → observe → reflect | JSON-RPC request/response/notification |
| State | Stateless per query | Stateful (memory stack) | Stateful sessions |
| Released | ~2020 | 2023–2025 | Nov 2024 (Anthropic) |

---

## 🗺️ Recommended Reading Order

1. Start with **RAG** to understand retrieval fundamentals.
2. Move to **Agentic RAG** to see how agents add reasoning/memory/tool-use.
3. Read **MCP** to learn the standard protocol agents use to connect to tools.
4. Finish with the **Relevance Graph** to see how a production system combines all three.
