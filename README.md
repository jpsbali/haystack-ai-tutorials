# Haystack AI RAG Tutorials

Comprehensive guide to building Retrieval-Augmented Generation (RAG) systems with Haystack AI - from fundamentals to production-ready implementations.

## Overview

This tutorial series provides in-depth, hands-on learning for building RAG applications using Haystack AI. Each notebook is self-contained and progressively builds your knowledge from basic RAG concepts to advanced production patterns.

**Target Audience:** Intermediate to advanced practitioners with basic understanding of:
- Python programming
- Machine learning concepts
- Large Language Models (LLMs)
- Embeddings and vector similarity

## What You'll Learn

### Fundamentals
- RAG architecture and core components
- Document stores and retrieval mechanisms
- Prompt engineering for RAG
- Building basic Q&A pipelines

### Advanced Retrieval
- Dense embeddings and semantic search
- Hybrid retrieval (BM25 + vector search)
- Query expansion techniques
- Reranking strategies for precision

### Agentic & Adaptive RAG
- Conditional routing and decision-making
- Web search fallback mechanisms
- Self-correcting RAG pipelines
- Conversational RAG with memory

### Specialized Techniques
- Corrective RAG (CRAG) patterns
- GraphRAG with knowledge graphs
- Long-context document handling
- Multimodal RAG (vision + text)


## Notebooks

1. **01_rag_fundamentals.ipynb** - RAG Fundamentals & Basic Implementation
   - Core RAG concepts and architecture
   - Building your first RAG pipeline
   - Prompt engineering basics
   - Simple Q&A systems

2. **02_advanced_retrieval.ipynb** - Advanced Retrieval Techniques
   - Semantic search with embeddings
   - Hybrid retrieval strategies
   - Query expansion
   - Reranking for improved precision

3. **03_agentic_rag.ipynb** - Advanced RAG Patterns & Agentic Behavior
   - Conditional routing
   - Web search fallback
   - Self-correcting pipelines
   - Conversational RAG with memory

4. **04_specialized_techniques.ipynb** - Specialized RAG Techniques
   - Corrective RAG (CRAG)
   - GraphRAG with Neo4j
   - Long-context handling
   - Multimodal RAG

## Prerequisites

### System Requirements
- **Python:** 3.9-3.12
- **RAM:** 8GB minimum (16GB recommended for local embeddings)
- **Disk Space:** 10GB+ for datasets and models
- **Internet:** Required for API calls and dataset downloads
- **Optional:** CUDA-capable GPU for local model inference

### Knowledge Prerequisites
- Intermediate Python programming
- Basic understanding of machine learning
- Familiarity with LLMs and embeddings
- Basic command line usage

## Setup Instructions

### 1. Clone or Download this Repository

```bash
cd haystack-ai-tutorials
```

### 2. Create a Virtual Environment

```bash
# Using venv
python -m venv venv

# Activate on macOS/Linux
source venv/bin/activate

# Activate on Windows
venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

**Note:** Installation may take 5-10 minutes depending on your internet connection.

### 4. Configure Environment Variables

```bash
# Copy the example environment file
cp .env.example .env

# Edit .env and add your API keys
# At minimum, you'll need:
# - OPENAI_API_KEY for most notebooks
# - COHERE_API_KEY for Notebook 2 (reranking)
# - SERPER_API_KEY for Notebook 3 (web search)
```

### 5. (Optional) Setup Neo4j for Notebook 4

For GraphRAG examples in Notebook 4, you'll need Neo4j:

**Option A: Docker (Recommended)**
```bash
docker run -d \
  --name neo4j \
  -p 7474:7474 -p 7687:7687 \
  -e NEO4J_AUTH=neo4j/your_password \
  neo4j:latest
```

**Option B: Desktop Installation**
Download from: https://neo4j.com/download/

### 6. Launch JupyterLab

```bash
jupyter lab
```

Your browser should open automatically. If not, navigate to: `http://localhost:8888`

## Getting Started

### Recommended Learning Path

1. **Start with Notebook 1** (01_rag_fundamentals.ipynb)
   - Even if you have RAG experience, this establishes the Haystack patterns used throughout

2. **Progress Sequentially** through Notebooks 2-3
   - Each builds on concepts from previous notebooks

3. **Notebook 4** can be done selectively
   - Choose based on your specific interests
   - Notebook 4: Advanced techniques (GraphRAG, multimodal)

### Running the Notebooks

Each notebook is self-contained:
- All imports and setup are included
- Data loading/generation is handled within the notebook
- No dependencies between notebooks
- Can be run independently in any order

**Estimated time per notebook:** 1-2 hours

## API Keys and Costs

### Required API Keys

| Provider | Notebooks | Cost | Get Key |
|----------|-----------|------|---------|
| OpenAI | 1, 2, 3, 4 | ~$1-5 per notebook | [platform.openai.com](https://platform.openai.com/api-keys) |
| Cohere | 2 | Free tier available | [dashboard.cohere.com](https://dashboard.cohere.com/api-keys) |
| SerperDev | 3 | Free tier (2500 queries) | [serper.dev](https://serper.dev/api-key) |

### Optional API Keys

- **Anthropic:** For using Claude models (alternative to OpenAI)
- **Hugging Face:** For downloading models/datasets

### Cost Optimization Tips

- Use smaller models during development (gpt-3.5-turbo vs gpt-4)
- Cache results to avoid repeated API calls
- Use local embeddings (sentence-transformers) instead of API-based
- Leverage free tiers when available

## Troubleshooting

### Common Issues

**1. Import Errors**
```bash
# Reinstall dependencies
uv pip install --upgrade -r requirements.txt
```

**2. API Key Errors**
- Verify your .env file has correct keys
- Ensure .env is in the same directory as notebooks
- Check API key validity on provider dashboards

**3. Memory Errors**
- Reduce batch sizes in notebooks
- Close other applications
- Consider using smaller datasets
- Use cloud notebooks (Google Colab, etc.)

**4. Neo4j Connection Issues**
- Verify Neo4j is running: `http://localhost:7474`
- Check credentials in .env file
- Ensure ports 7474 and 7687 are not in use

### Getting Help

- **Haystack Documentation:** https://docs.haystack.deepset.ai/
- **Haystack Discord:** https://discord.gg/haystack
- **GitHub Issues:** Report issues specific to these tutorials

## Project Structure

```
haystack-ai-tutorials/
├── README.md                          # This file
├── requirements.txt                   # Python dependencies
├── .env.example                       # Environment variables template
├── .env                              # Your API keys (create this)
├── 01_rag_fundamentals.ipynb
├── 02_advanced_retrieval.ipynb
├── 03_agentic_rag.ipynb
├── 04_specialized_techniques.ipynb
```

## Additional Resources

### Official Documentation
- [Haystack Documentation](https://docs.haystack.deepset.ai/)
- [Haystack Tutorials](https://haystack.deepset.ai/tutorials)
- [Haystack API Reference](https://docs.haystack.deepset.ai/reference)

### Research Papers
- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401)
- [Self-RAG: Learning to Retrieve, Generate, and Critique](https://arxiv.org/abs/2310.11511)
- [Corrective Retrieval Augmented Generation](https://arxiv.org/abs/2401.15884)

### Community
- [Haystack GitHub](https://github.com/deepset-ai/haystack)
- [Haystack Discord Community](https://discord.gg/haystack)
- [DeepSet Blog](https://www.deepset.ai/blog)

### Related Tools
- [RAGAS Evaluation Framework](https://docs.ragas.io/)
- [LangChain](https://python.langchain.com/)
- [LlamaIndex](https://www.llamaindex.ai/)

## Success Criteria

After completing these tutorials, you should be able to:

- ✅ Build production-ready RAG systems from scratch
- ✅ Choose appropriate retrieval strategies for your use case
- ✅ Implement advanced patterns (agentic, corrective, graph-based RAG)
- ✅ Comprehensively evaluate RAG system performance
- ✅ Handle edge cases and failure modes gracefully
- ✅ Stay current with RAG research and best practices

## Contributing

Found an issue or have a suggestion? Contributions are welcome!

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- **DeepSet AI** for creating and maintaining Haystack
- **OpenAI, Cohere, Anthropic** for LLM APIs
- **RAGAS team** for evaluation framework
- **Research community** for advancing RAG techniques

## Citation

If you use these tutorials in your work, please cite:

```bibtex
@misc{haystack-rag-tutorials,
  title={Comprehensive Haystack AI RAG Tutorials},
  author={A-Stack AI},
  year={2025},
  url={https://github.com/yourusername/haystack-ai-tutorials}
}
```

---

**Ready to get started?** Open `01_rag_fundamentals.ipynb` and begin your RAG journey!

For questions or feedback, reach out via GitHub Issues or the Haystack Discord community.

Happy learning! 🚀
