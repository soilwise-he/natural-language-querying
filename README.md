# NATURAL LANGUAGE QUERYING (NLQ) - T3.3
Application component that provides Natural Language Querying (NLQ) services, making knowledge stored in a graph database accessible for e.g. a ChatBot UI.

## Purpose
Natural language quering (NLQ) in general enables users to interact with complex database. Including NoSQL databases, such as Knowledge Graphs. NLQ systems can be seen as a subset of Question-Answering (QA) systems, which ar designed to answer questions posed by users in natural language. The overall goal is to enhance knowledge discovery and enable non-technical users to benefit from all the information for knowledge-driven decision-making.

## Out-of-Scope
- This component will only provide NLQ services, it will not include a graphical user interface such as a ChatBot.
- This component is not intended to use LLMs to assist in creation and curation of KGs or ontologies.

Note that in issue [#5][i5] it is discussed to still add a simple [chainlit](https://chainlit.io) based UI to the component for prototype / demo purpose only.

## Description
The research field of NLQ is currently dominated by approaches using Large Language Models (LLMs) to understand human questions and provide natural language answers. LLMs and conversational interfaces (e.g. ChatBots) can be beneficial for exploring and extracting information from (extremely) large knowledge structures.

NLQs using LLMs can be implemented in a number of ways:
- Retrieval Augmented Generation (RAG) systems, that enhance the grounding context of an LLM for covering questions specific to a domain or proprietary knowledge. A RAG implementation needs various subcomponents, such as an LLM and a vector database.
- Using an LLM to translate questions into structured database queries, e.g. using SPARQL or Cypher. Various methods can be used to improve the queries that are created and avoid hallucinations, e.g. few shot prompts, using a LLM that is trained for creating code, or providing the ontology as part of RAG.
- Fine-tuning a custom LLM with proprietary data and/or knowledge graphs. This is usally the most costly option, requiring sufficient and curated training data and substantial compute time. It is also inflexible, since the KG gets 'baked-in' to the LLM. A possible benefit is that it creates a local custom LLM that can give the best performance for a specific task or knowledge domain.

Known challenges:
- Contextual understanding
- Complex query interpretation
- Challenges in modeling and storing data
- Transparency and trustworthiness

See issue [#2][i2] for the discussion on, and selection of the initial concept implementation.

> Following the (Brugge) architecture, the LLM component only interacts with the triple store, using SPARQL queries. So at first it can work with text and relations it can retrieve from there. After the user selects one or more documents these can be retrieved and used as input for RAG. Importing documents into a vector store can take a few minutes (depending on size of the documents, embedding model used, and hardware configuration). After that the user can 'talk' with these documents to have more detailed access to the knowledge contained within them.

> To avoid spending a lot of time perfecting the generation of SPARQL queries by the LLM, we can use known fixed queries and have the LLM use them via "tool calling".

## Supported (human) languages
The aim is to prefer the use of multilingual NLP components as much as possible, e.g. embedding models that are multilingual, and LLMs that have been trained on not only english text. Even though at first most knowledge and human input will be in English, it is expected that users will request support for other languages as well. (See issue [#13][i13])

## Tech
The initial focus will be on teaching the machine to generate usable and proper graph queries, most likely SPARQL and perhaps also Cypher (Neo4J). It might be the case the a specific query language and graph database type performs significantly better than the other, this will have to be tested.

The LLM framework to be used is [LangChain](https://www.langchain.com) (Python), or its Java version [LangChain4J](https://docs.langchain4j.dev). Depending on the (non-functional) requirements for the component. As alternative framework [LlamaIndex](https://www.llamaindex.ai) can be considered.

Research around Large Language Models currently happens at a high pace, with new models being released frequently. At first a simple (relatively low number of trainable parameters) LLM can be used in development. Once an initial prototype is in place that allows validating prompts - expected answers, comparisions between LLMs can be performed and the best suited model selected. A good resource for open LLMs and their performance is this [Huggingface open LLM leaderboard](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard). 

The API will be a (traditional) web service that can receive questions (prompts) and provide responses (in streaming mode).

## Hardware
Depending on the chosen LLM (size / number of parameters) and its usage (tokens in/out, number of requests/sec, etc.) specific hardware might be needed to implement a usable service. E.g. one or more computers/nodes with medium or high end GPUs can be required, as well as a load balancer. Another option is to make use of a hosted LLM service, with usually a pay-per-use subscription. Some LLMs (and vector stores) are available as Docker containers.

---

[i2]: https://github.com/soilwise-he/natural-language-querying/issues/2
[i5]: https://github.com/soilwise-he/natural-language-querying/issues/5
[i13]: https://github.com/soilwise-he/natural-language-querying/issues/13
