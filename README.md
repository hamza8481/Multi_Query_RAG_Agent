Advanced Multi-Query RAG AI Agent

An advanced, Langchain-powered conversational AI agent built in n8n. This workflow employs a sophisticated Retrieval-Augmented Generation (RAG) pattern to ensure accurate, contextually relevant responses derived strictly from your internal vector database.

It breaks complex user prompts into discrete sub-queries, executes vector searches in parallel, filters results by relevance thresholds, and utilizes internal AI reasoning to synthesize the final answer.

Business and Operational Value
1. High-Fidelity Retrieval: Avoids the common pitfall of simplistic vector searches by decomposing queries, leading to fewer hallucinations and higher recall on multi-part questions.
2. Data Quality Control: Implements a strict similarity score threshold to ensure the LLM only receives highly relevant context.
3. Transparency and Reasoning: Uses a specialized reasoning tool to analyze retrieved content before generating the final response.

Tech Stack and Key Nodes
1. Framework: n8n Advanced AI (Langchain) nodes.
2. LLM and Embeddings: OpenAI (gpt-4o-mini for chat, OpenAI embeddings).
3. Vector Database: Supabase (pgvector).
4. Core Nodes:
   a. AI Agent: The central orchestrator with short-term buffer memory.
   b. Tool - Query knowledge base: Sub-workflow router that executes the RAG retrieval.
   c. Think Tool: Enables pre-response critical analysis.

Execution Flow
1. Trigger: A user submits a query via the Chat Interface.
2. Decomposition: The AI Agent assesses the question and generates 1 to 5 sub-queries.
3. Retrieval: Sub-queries are split and passed to Supabase to fetch vector-matched document chunks.
4. Filtering: Chunks are formatted. Any chunk with a similarity score less than 0.4 is discarded.
5. Reasoning: The agent receives the aggregated high-quality chunks and uses the Think tool to mentally map the answer.
6. Synthesis: The finalized answer is delivered back to the user interface.
