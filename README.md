# Collaborative Multi-Agent System
This project implements a collaborative multi-agent system using LangGraph, where Researcher and Coder agents work together to address complex user queries. Instead of a single supervisor, these agents are designed to communicate and pass information between each other, iteratively refining their outputs until a comprehensive solution is achieved.

## Project Description
In many real-world scenarios, a single AI agent cannot efficiently solve problems that require diverse skill sets. This project demonstrates a more dynamic approach where specialized agents collaborate:

Researcher Agent: Focuses on gathering and synthesizing information from external sources.

Coder Agent: Focuses on generating, executing, and refining code to solve problems or demonstrate concepts.

The system operates on a principle of shared responsibility and iterative refinement. Agents pass their findings and requests to each other, allowing for a fluid workflow that adapts to the needs of the query. This collaborative model is particularly effective for tasks that require both extensive knowledge retrieval and practical code-based solutions.

## Technologies Used
Python: The core programming language for the entire system.

LangChain: A framework for developing applications powered by large language models, used here for building the individual agents and their capabilities.

LangGraph: An extension of LangChain specifically designed for building stateful, multi-actor applications with LLMs, enabling the complex collaborative workflow and conditional routing between agents.

OpenAI GPT-4: The powerful Large Language Model (LLM) used across both agents for understanding queries, generating responses, making decisions, and producing/interpreting code.

Tavily Search API: Integrated within the Researcher agent to provide real-time, relevant information retrieval from the web.

PythonREPL: Used by the Coder agent to execute generated Python code and return results, allowing for verification and debugging.

## Architecture and Workflow
The collaborative multi-agent system's workflow is defined as a graph that emphasizes interaction and hand-offs between the Researcher and Coder agents. The agents communicate and iterate until the query is fully addressed.

![image](https://github.com/user-attachments/assets/b42a4030-440e-41de-94d8-962b67381263)


START Node: The initial entry point where the user's query is received. The query is typically first directed to the RESEARCHER to gather initial context or information.

RESEARCHER Node:

Function: Gathers information from the web using Tavily Search API based on the user's query or a request from the CODER.

Output & Hand-off:

If the research provides sufficient information to answer the query directly, it can route to END.

If the query requires a code-based solution, or if the CODER needs more context to write code, the RESEARCHER synthesizes its findings and passes the task to the CODER.

It can also identify if no further research is possible or if the information is sufficient for the CODER.

CODER Node:

Function: Generates Python code to address the query, potentially based on information provided by the RESEARCHER.

Execution & Evaluation: Executes the generated code using PythonREPL to test its functionality and verify results.

Output & Hand-off:

If the code successfully solves the problem and the answer is complete, it can route to END.

If the code execution reveals a need for more information, clarification, or a different approach (e.g., an API key is missing, or the research was insufficient), the CODER can formulate a new research query and pass the task back to the RESEARCHER. This creates the collaborative loop.

END Node:

The termination point of the graph. Either the RESEARCHER or CODER can determine that the task is complete and the final answer is ready, routing the flow to END.

