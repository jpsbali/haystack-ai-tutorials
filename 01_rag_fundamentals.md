# 📘 Notebook 1: RAG Fundamentals & Basic Implementation - Overview

## 🎯 Learning Objectives

This notebook provides a comprehensive introduction to Retrieval-Augmented Generation (RAG) systems:

- **Understand core RAG architecture** and components
- **Implement basic RAG pipelines** using Haystack
- **Work with document stores, retrievers, and generators**
- **Master prompt engineering** for RAG applications
- **Understand when to use RAG vs fine-tuning**

**Duration:** 90-120 minutes  
**Level:** Intermediate

---

## 📚 Main Sections

### **1. Introduction to RAG**

**What is RAG?**
- Combines Large Language Models (LLMs) with external knowledge retrieval
- Addresses LLM limitations: knowledge cutoffs, hallucinations, domain-specific needs

**Why RAG?**
| Problem | RAG Solution |
|---------|-------------|
| LLMs have knowledge cutoff dates | Access to up-to-date information |
| LLMs can hallucinate facts | Grounded responses with source citations |
| Domain-specific knowledge needed | Connect to proprietary knowledge bases |
| Expensive to fine-tune for every update | Simply update document store |

**RAG vs Fine-Tuning Decision Guide:**
- **Use RAG when:** Information changes frequently, need citations, document-based knowledge
- **Use Fine-Tuning when:** Need specific tone/style, specialized reasoning, stable knowledge

**Basic RAG Architecture:**
```
User Query → Retriever → Relevant Docs → Prompt + Docs → LLM → Answer
                ↑
           Document Store
```

---

### **2. Environment Setup**

- Imports Haystack core components
- Configures OpenAI API keys
- Sets up document stores, retrievers, prompt builders, and generators
- Prepares the development environment

---

### **3. Understanding RAG Components**

Deep dive into each component with hands-on examples:

#### **3.1 Document Representation**
- Uses Haystack's `Document` dataclass
- Stores content and metadata (source, category, date, etc.)
- Each document gets a unique ID

#### **3.2 Document Store**
- `InMemoryDocumentStore` for simple storage
- Stores and manages all documents
- Supports filtering and counting operations

#### **3.3 Retriever**
- `InMemoryBM25Retriever` for keyword-based retrieval
- Finds relevant documents based on query
- Returns documents with relevance scores

#### **3.4 Prompt Builder**
- Uses Jinja2 templates to construct prompts
- Combines query with retrieved documents
- Flexible template system for different use cases

#### **3.5 Generator**
- `OpenAIGenerator` for answer generation
- Takes prompt and generates natural language response
- Configurable temperature and model parameters

---

### **4. Data Preparation**

Helper functions to generate sample datasets:
- Company knowledge base (HR policies, benefits, procedures)
- Python documentation (programming concepts)
- News articles (current events)

---

### **5. Example 1: Simple Q&A System**

**Goal:** Build a complete RAG pipeline for company policy questions

**Implementation:**
1. **Create Pipeline Components**
   - Initialize document store with company policies
   - Set up retriever, prompt builder, and LLM

2. **Build the RAG Pipeline**
   - Connect components using Haystack's Pipeline
   - Define data flow: retriever → prompt_builder → llm

3. **Test the Pipeline**
   - Sample questions: vacation days, remote work, health insurance
   - Displays answers with response times and retrieved documents

**Key Features:**
- Professional HR assistant persona
- Clear, concise answers based on policies
- Source citation with policy titles
- Friendly and professional tone

---

### **6. Example 2: Technical Documentation Assistant**

**Goal:** Build a RAG system for Python programming questions

**Dataset:**
- Python documentation covering:
  - Error handling (try-except blocks)
  - File operations (with statements)
  - List comprehensions
  - Generators and iterators
  - Decorators and context managers

**Implementation:**
- Similar pipeline structure to Example 1
- Technical tone adapted for programming queries
- Code examples in responses

**Sample Queries:**
- "How do I handle errors in Python?"
- "What's the difference between a list comprehension and a generator?"
- "How do I read a file safely?"

---

### **7. Example 3: News Article Summarization with Citations**

**Goal:** Answer questions about news with proper source attribution

**Dataset:**
- News articles covering:
  - Quantum computing breakthroughs
  - Climate agreements
  - AI in medical diagnosis
  - Electric vehicle trends

**Key Features:**
- Includes source URLs and publication dates
- Structured citation format
- Clear attribution to original sources
- Informative tone for news content

**Template Enhancements:**
- Explicit citation requirements
- Source URL inclusion
- Date-based context

---

### **8. Prompt Engineering Best Practices**

**Explores different prompt structures:**

1. **Basic Prompt**
   - Simple context + question format
   - Minimal instructions

2. **Structured Prompt**
   - Numbered context sections
   - Clear formatting

3. **With Instructions**
   - Explicit guidelines for the LLM
   - Constraints on behavior
   - Citation requirements

4. **Chain of Thought**
   - Step-by-step reasoning
   - Encourages thoughtful analysis

**Key Insights:**
- Clear instructions improve answer quality
- Structure helps LLM parse information
- Constraints prevent hallucination
- Chain of thought improves accuracy
- Citation requirements ensure transparency

---

### **9. Basic Evaluation**

**Implements evaluation metrics:**

#### **Retrieval Precision**
- Measures if retrieved documents are relevant
- Compares expected vs actual retrieved documents
- Calculates precision percentage

#### **Test Cases**
- Predefined query-document pairs
- Expected relevant documents for each query
- Automated evaluation across multiple queries

**Evaluation Results:**
- Average precision scores
- Per-query analysis
- Identification of retrieval gaps

---

### **10. Exercises & Challenges**

#### **Exercise 1: Add More Documents** ✅ IMPLEMENTED
**Goal:** Extend the company knowledge base

**Implementation:**
- Added 5 new policies:
  - Parental Leave Policy (16 weeks primary, 8 weeks secondary)
  - Referral Bonus Program ($3,000 structure)
  - Office Amenities (gym, meals, charging stations)
  - Relocation Assistance (up to $10,000)
  - Flexible Work Hours (core hours 10 AM - 3 PM)
- Tested retrieval with relevant queries
- Verified RAG system handles new documents correctly

---

#### **Exercise 2: Improve Prompt Template** ✅ IMPLEMENTED
**Goal:** Create enhanced prompt with confidence ratings and structured output

**Implementation:**
- **Confidence Rating (1-10):** Indicates answer certainty
- **Short Answer:** Quick 1-2 sentence summary
- **Detailed Explanation:** Comprehensive information
- **Sources Used:** Lists relevant documents

**Benefits:**
- Better user experience with structured responses
- Increased transparency and trust
- Easier verification against sources
- Confidence scores identify uncertainty

**Comparison:**
- Side-by-side testing with basic template
- Shows improvements in clarity and usefulness
- Demonstrates professional response format

---

#### **Exercise 3: Handle Out-of-Scope Questions** ✅ IMPLEMENTED
**Goal:** Properly reject questions outside the knowledge base

**Testing Phase:**
- Out-of-scope questions: weather, cooking, stocks, sports, general knowledge
- Analyzes basic pipeline behavior with irrelevant queries

**Issues Identified:**
- System may attempt to answer using irrelevant documents
- Risk of hallucination based on general knowledge
- No clear indication when information is unavailable
- Low relevance scores but documents still used

**Improved Solution:**
- Explicit scope definition (TechCorp policies only)
- Structured rejection responses for out-of-scope questions
- Lower temperature (0.1) for consistent boundary enforcement
- Helpful guidance directing users to appropriate resources
- Handles both completely out-of-scope and missing info scenarios

**Validation:**
- Tests improved pipeline with same out-of-scope questions
- Verifies in-scope questions still work correctly
- Ensures accuracy while enforcing boundaries

---

#### **Challenge: Build a Multi-Topic RAG System** ✅ IMPLEMENTED
**Goal:** Combine multiple knowledge bases with automatic routing

**Implementation:**

1. **Unified Document Store**
   - Combined 3 knowledge bases (company policies, Python docs, news)
   - Enhanced metadata with topic and domain tags
   - Single source of truth for all information

2. **Intelligent Query Routing**
   - `classify_query()` function with keyword-based classification
   - Scores against three categories
   - Automatic determination of relevant knowledge base
   - Fallback logic for ambiguous queries

3. **Filtered Retrieval**
   - Uses metadata filters to search specific topics
   - Improves precision by focusing on correct domain
   - Reduces noise from irrelevant documents

4. **Adaptive Response System**
   - `ask_unified_question()` function handles end-to-end flow
   - Classifies query → Retrieves filtered docs → Builds context-aware prompts
   - Generates answers with source attribution
   - Returns comprehensive results with topic, domain, and timing

5. **Comprehensive Testing**
   - 6 test questions across all three domains
   - Displays classification, domain, answer, and sources
   - Validates routing accuracy

**Key Features:**
- Single unified interface for multiple domains
- Automatic routing eliminates user domain specification
- Scalable architecture for adding new topics
- Better accuracy through focused retrieval
- Clear provenance with source tracking

---

### **11. Summary & Next Steps**

**What You've Learned:**

✅ **RAG Fundamentals**
- What RAG is and when to use it
- Core components and their interactions
- Pipeline architecture

✅ **Practical Implementation**
- Built 3 different RAG systems (HR, documentation, news)
- Worked with real-world use cases
- Handled different document types

✅ **Prompt Engineering**
- Compared different prompt structures
- Learned best practices for RAG prompts
- Implemented confidence ratings and citations

✅ **Evaluation Basics**
- Measured retrieval precision
- Evaluated system performance
- Identified improvement areas

✅ **Advanced Patterns**
- Out-of-scope question handling
- Multi-topic routing
- Unified knowledge base management

---

## 🔑 Key Concepts

### **RAG Pipeline Flow**
```
1. User asks question
2. Retriever finds relevant documents from store
3. Prompt Builder combines query + documents
4. LLM Generator produces answer
5. User receives response with citations
```

### **Core Components**
- **Document Store:** Storage layer for all documents
- **Retriever:** Search engine (BM25 for keyword matching)
- **Prompt Builder:** Template engine for context construction
- **Generator:** LLM for natural language generation
- **Pipeline:** Orchestration layer connecting components

### **Best Practices**
1. **Clear Instructions:** Tell LLM what to do and what not to do
2. **Structure:** Format context for easy parsing
3. **Constraints:** Prevent hallucination and out-of-scope answers
4. **Citations:** Always include source attribution
5. **Evaluation:** Measure and improve retrieval quality

---

## 💡 Practical Applications

This notebook teaches you to build:
- **Internal knowledge bases** (HR policies, documentation)
- **Customer support systems** (FAQ, troubleshooting)
- **Documentation assistants** (technical guides, manuals)
- **News/research summarization** (with citations)
- **Multi-domain Q&A systems** (unified interface)

---

## 🚀 What's Next?

After mastering these fundamentals, you're ready for:
- **Notebook 2:** Advanced retrieval (semantic search, hybrid retrieval, reranking)
- **Notebook 3:** Agentic RAG (conditional routing, self-correction, conversational memory)
- **Notebook 4:** Specialized techniques (CRAG, GraphRAG, multimodal RAG)

---

## 📊 Skills Acquired

By completing this notebook, you can now:
- ✅ Build production-ready RAG systems from scratch
- ✅ Choose appropriate components for your use case
- ✅ Engineer effective prompts for RAG applications
- ✅ Handle out-of-scope queries gracefully
- ✅ Implement multi-domain knowledge systems
- ✅ Evaluate and improve retrieval quality
- ✅ Add proper source attribution and citations

---

## 🎓 Difficulty Progression

**Beginner → Intermediate → Advanced**

This notebook takes you from:
- Understanding what RAG is
- Building your first simple pipeline
- Implementing production patterns (multi-topic routing, out-of-scope handling)

Perfect foundation for advanced RAG techniques in subsequent notebooks!
