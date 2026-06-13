# RAG · Agentic RAG · MCP — Relevance Graph & Learning Map

This document visualizes how **RAG**, **Agentic RAG**, and **MCP** relate to each other conceptually, architecturally, and as a learning path.

---

## 1. The Big Picture — One Diagram

```mermaid
flowchart TB
    subgraph L1["LEVEL 1 — FOUNDATION"]
        RAG["📚 RAG (Simple)<br/>Retrieval + Generation<br/>Embeddings · Chunking · Vector DBs · Reranking"]
    end

    subgraph L2["LEVEL 2 — INTELLIGENCE"]
        ARAG["🤖 Agentic RAG<br/>Planning · Reflection · Tool Use · Multi-Agent<br/>Memory · Workflow Orchestration"]
    end

    subgraph L3["LEVEL 3 — CONNECTIVITY"]
        MCP["🔌 MCP (Model Context Protocol)<br/>Standardized Tools · Resources · Prompts<br/>Host · Client · Server architecture"]
    end

    RAG -->|"adds reasoning,<br/>planning & tool-use<br/>on top of retrieval"| ARAG
    ARAG -->|"needs a standard way to<br/>call tools & data sources"| MCP
    MCP -->|"a RAG pipeline can live<br/>BEHIND an MCP server<br/>as a Resource provider"| RAG
    MCP -->|"gives agentic patterns<br/>(tool use, multi-agent,<br/>sampling) a common wire format"| ARAG
```

---

## 2. Conceptual Relevance Map

```mermaid
mindmap
  root((AI Context & Agent Stack))
    RAG
      Embeddings & Tokenization
      Chunking Strategies
      Vector Databases
      Reranking
      Naive / Hybrid / Hierarchical / HyDE / Reference-based
    Agentic RAG
      Reflection
      Planning
      Tool Use
      Multi-Agent
      Memory Stack
        Episodic
        Semantic
        Procedural
        In-Context
      Workflow Patterns
        Prompt Chaining
        Routing
        Parallelization
        Orchestrator-Workers
        Evaluator-Optimizer
    MCP
      Host-Client-Server
      Tools / Resources / Prompts
      Roots & Sampling
      JSON-RPC Lifecycle
      WebMCP
      Security & Trust
```

---

## 3. How They Solve Each Other's Limitations

```mermaid
flowchart LR
    subgraph Problem1["RAG's limitation"]
        P1["Single-shot pipeline:<br/>query → retrieve → generate<br/>No multi-hop reasoning,<br/>no self-correction"]
    end
    subgraph Solution1["Solved by Agentic RAG"]
        S1["Agent loop: plan → act →<br/>observe → reflect<br/>Multi-step retrieval,<br/>self-correction, tool use"]
    end
    subgraph Problem2["Agentic RAG's limitation"]
        P2["Every tool/API integration<br/>is bespoke per agent<br/>(N×M problem)"]
    end
    subgraph Solution2["Solved by MCP"]
        S2["Standard protocol:<br/>any agent (client) ↔<br/>any tool (server)<br/>N+M, plug-and-play"]
    end

    P1 --> S1
    S1 --> P2
    P2 --> S2
    S2 -.->|"servers can wrap<br/>RAG pipelines as<br/>Resources"| P1
```

---

## 4. Architectural Layering — How a Production System Combines All Three

```mermaid
flowchart TB
    U["👤 User Query"] --> H["🏠 Host Application<br/>(Claude Desktop / Custom Agent UI)"]
    H --> A["🤖 Agentic RAG Layer<br/>Planner → Reflector → Tool-caller<br/>Memory Stack (episodic/semantic/procedural)"]

    A -->|"MCP Client"| MC1["🔗 MCP Client → Vector DB Server"]
    A -->|"MCP Client"| MC2["🔗 MCP Client → Web Search Server"]
    A -->|"MCP Client"| MC3["🔗 MCP Client → Internal API Server"]

    MC1 --> VDB["🗄 Vector DB<br/>(Qdrant/Pinecone/Weaviate)<br/>RAG retrieval pipeline:<br/>Embed → Search → Rerank"]
    MC2 --> WS["🌐 Live web results"]
    MC3 --> API["🏢 ERP / CRM / Ticketing"]

    VDB --> A
    WS --> A
    API --> A

    A --> ANS["✓ Grounded, multi-step,<br/>tool-verified answer + trace"]
```

**Reading this diagram:**
1. The **Host** (e.g., Claude Desktop) receives the user query.
2. The **Agentic RAG layer** plans the task, decides what context/tools are needed, and loops through reflection if needed.
3. Each external capability — a vector database, web search, or internal business system — is exposed via an **MCP server**, accessed through an **MCP client**.
4. The **RAG pipeline itself** (embedding → retrieval → reranking, from the first guide) lives *inside* the Vector DB MCP server as a Resource/Tool provider.
5. Results flow back through the agent's memory and reasoning loop to produce a final, grounded, cited answer.

---

## 5. Side-by-Side Comparison Table

| Dimension | RAG (Simple) | Agentic RAG | MCP |
|---|---|---|---|
| **Core question answered** | "How do I ground an LLM's answer in external knowledge?" | "How do I make retrieval & reasoning multi-step, self-correcting, and tool-using?" | "How do I let any AI app talk to any tool/data source without bespoke code?" |
| **Unit of work** | One-shot retrieve → augment → generate | Agent loop: plan → act → observe → reflect | Request/Response/Notification over JSON-RPC 2.0 |
| **Key components** | Embeddings, chunking, vector DB, reranker | Planner, Reflector, Memory stack, Multi-agent orchestrator | Host, Client, Server, Tools/Resources/Prompts |
| **State** | Stateless per query | Stateful via Memory Stack (episodic/semantic/procedural/in-context) | Stateful sessions (moving toward stateless/handle-based in 2026 RC) |
| **Failure mode addressed** | Hallucination, stale knowledge, no citations | Single-shot pipelines that can't handle multi-hop tasks | N×M integration explosion, fragmented tool access |
| **Released / popularized** | ~2020 (Lewis et al., "Retrieval-Augmented Generation" paper) | 2023–2025 (Self-RAG, ReAct, AutoGPT-style agents) | November 2024 (Anthropic) |
| **Analogy** | "Open-book exam" for the LLM | "A researcher with a notebook and a plan" | "USB-C port for AI applications" |

---

## 6. Suggested Learning Path (Recap)

```mermaid
flowchart LR
    A["1️⃣ RAG Basics<br/>Embeddings, Chunking,<br/>Vector DBs, Reranking"] --> B["2️⃣ Agentic Patterns<br/>Reflection, Planning,<br/>Tool Use, Multi-Agent"]
    B --> C["3️⃣ MCP<br/>Host/Client/Server,<br/>Tools/Resources/Prompts"]
    C --> D["4️⃣ Combine All Three<br/>Production agentic RAG<br/>systems connected via MCP"]
```

| Stage | Read | Focus |
|---|---|---|
| 1 | [RAG — Zero to Hero](rag-zero-to-hero.md) | Understand retrieval fundamentals: how LLMs get grounded in external data |
| 2 | [Agentic RAG — Zero to Hero](agentic-rag-zero-to-hero.md) | Learn how agents add reasoning, planning, memory, and tool use on top of RAG |
| 3 | [MCP — Zero to Hero](MCP-zero-to-hero.md) | Learn the standard protocol that lets agents connect to tools and data sources |
| 4 | — | Combine: build agentic RAG systems where every external capability (vector DB, APIs, web search) is exposed as an MCP server |

---

## 7. Quick-Reference Glossary Across All Three Guides

| Term | Appears In | Definition |
|---|---|---|
| **Embedding** | RAG | Dense vector representation of text capturing semantic meaning |
| **Reranker** | RAG | Second-stage model that re-scores retrieved candidates for precision |
| **Reflection** | Agentic RAG | Agent self-critiques and revises its own output in a loop |
| **Orchestrator** | Agentic RAG, MCP | A coordinating agent/process that delegates to specialist workers or servers |
| **Memory Stack** | Agentic RAG | Episodic, semantic, procedural, and in-context memory tiers |
| **Tool** | Agentic RAG, MCP | A callable function/action the model or agent can invoke |
| **Resource** | MCP | Read-only addressable data exposed by an MCP server |
| **Sampling** | MCP | A server asking the client to run an LLM completion on its behalf |
| **JSON-RPC 2.0** | MCP | The wire protocol underlying all MCP communication |
| **HyDE** | RAG | Hypothetical Document Embeddings — draft a hypothetical answer to bridge query/document vocabulary gaps |
| **ADW** | Agentic RAG | Agentic Document Workflows — end-to-end document automation with state and business rules |
