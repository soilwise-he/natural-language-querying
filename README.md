# large-language-model
Application component that provides chatbot like UI services while accessing the triple store via a query language. 

The initial focus will be on teaching the machine to generate usable and proper graph queries, most likely SPARQL and perhaps also Cypher (Neo4J). The LLM framework to be used is LangChain (Python), or its Java version LangChain4J. Depending on the (non-functional) requirements for the component.

The API will be a (traditional) web service that can receive questions (prompts) and provide responses (in streaming mode).
