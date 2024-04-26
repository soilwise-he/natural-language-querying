# large-language-model
Application component that provides Natural Language Querying (NLQ) services, making knowledge stored in a graph database accessible for e.g. a ChatBot UI.

## Purpose
Natural language quering (NLQ) in general enables users to interact with complex database. Including NoSQL databases, such as Knowledge Graphs. NLQ systems can be seen as a subset of Question-Answering (QA) systems, which ar designed to answer questions posed by users in natural language. The overall goal is to enhance knowledge discovery and enable non-technical users to benefit from all the information for knowledge-driven decision-making.

## Out-of-Scope
- This component will only provide NLQ services, it will not include a graphical user interface such as a ChatBot.
- This component is not intended to use LLMs to assist in creation and curation of KGs or ontologies.

## Description
The research field of NLQ is currently dominated by approaches using Large Language Models (LLMs) to understand human questions and provide natural language answers. LLMs and conversational interfaces (e.g. ChatBots) can be beneficial for exploring and extracting information from (extremely) large knowledge structures.

NLQs using LLMs can be implemented in a number of ways:
- Retrieval Augmented Generation (RAG) systems, that enhance the grounding context of an LLM for covering questions specific to a domain or proprietary knowledge. A RAG implementation needs various subcomponents, such as an LLM and a vector database.
- Using an LLM to translate questions into structured database queries, e.g. using SPARQL or Cypher. Various methods can be used to improve the queries that are created and avoid hallucinations, e.g. few shot prompts, using a LLM that is trained for creating code, or providing the ontology as part of RAG.
- Fine-tuning a custom LLM with proprietary data, usually the most costly option.

Known challenges:
- Contextual understanding
- Complex query interpretation
- Challenges in modeling and storing data
- Transparency and trustworthiness

## Tech
The initial focus will be on teaching the machine to generate usable and proper graph queries, most likely SPARQL and perhaps also Cypher (Neo4J). 

The LLM framework to be used is LangChain (Python), or its Java version LangChain4J. Depending on the (non-functional) requirements for the component. Research around Large Language Models currently happens at a high pace, with new models being released frequently. At first a simple (relatively low number of trainable parameters) LLM can be used in development. Once an initial prototype is in place that allows validating prompts - expected answers, comparisions between LLMs can be performed and the best suited model selected. 

The API will be a (traditional) web service that can receive questions (prompts) and provide responses (in streaming mode).
