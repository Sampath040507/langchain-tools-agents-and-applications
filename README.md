# langchain-tools-agents-and-applications
Hands-on implementations of LangChain tools, tool calling, and AI agents, covering built-in and custom tools, currency conversion application, and agent workflows using ReAct and the newer `create_agent()` API.

## Overview

This repository contains hands-on explorations and practical implementations of LangChain tools, tool calling, and AI agents.

It starts with the fundamentals of defining and using tools, progresses to connecting tools with language models, and then explores how AI agents use tools to accomplish tasks. Along the way, the concepts are applied through practical examples such as a currency conversion application that retrieves live exchange rates through an external API.

The repository also explores the transition from the legacy ReAct agent implementation using `AgentExecutor` to the newer `create_agent()` interface.

## Table of Contents

- [Technologies & Tools](#technologies--tools)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Learning Path and Implementations](#learning-path-and-implementations)
  - [1. Tools](#1-tools)
  - [2. Tool Calling](#2-tool-calling)
  - [3. Currency Conversion Application](#3-currency-conversion-application)
  - [4. AI Agents](#4-ai-agents)
- [Understanding the Agent Implementation Progression](#understanding-the-agent-implementation-progression)
- [Environment Variables and API Keys](#environment-variables-and-api-keys)
- [Further Improvements](#further-improvements)

## Technologies & Tools

The following technologies, libraries, and external services are used across the implementations.

| Category | Technologies / Tools |
|---|---|
| Programming Language | Python |
| Framework | LangChain |
| Language Models | OpenAI Chat Models (`ChatOpenAI`) |
| Tool Development | `@tool`, `StructuredTool`, `BaseTool` |
| Tool Integration | Tool Binding, Tool Calling, `InjectedToolArg` |
| Agent Development | ReAct Agents, `AgentExecutor`, `create_agent()` |
| Search | DuckDuckGo Search |
| External APIs | ExchangeRate API, Weatherstack API |
| HTTP Requests | Requests |
| Data Validation | Pydantic |
| Development Environment | Jupyter Notebook |

## Repository Structure

```text
langchain-tools-agents-and-applications/
│
├── 1_tools_langchain.ipynb
│
├── 2_tool_calling_langchain.ipynb
├── 2.1_currency_conversion_tool_langchain.ipynb
│
├── 3.0_agent_langchain.ipynb
├── 3.1_agent_langchain_withupdation.ipynb
├── 3.2_agent_langchain_newapproach.ipynb
│
├── README.md
├── requirements.txt
├── .env.example
└── .gitignore
```

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/langchain-tools-agents-and-applications.git
cd langchain-tools-agents-and-applications
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it:

**Windows (Command Prompt):**

```bash
.venv\Scripts\activate
```

**Windows (PowerShell):**

```powershell
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
source .venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure API keys

Create a `.env` file in the root directory and add the required API keys.

Refer to the [Environment Variables and API Keys](#environment-variables-and-api-keys) section for details.

### 5. Run the notebooks

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open the notebook you want to explore and execute its cells sequentially.

## Learning Path and Implementations

### 1. Tools

**Notebook:** `1_tools_langchain.ipynb`

Explores how tools extend the capabilities of language models by allowing them to interact with external functions and services.

Topics covered:

- Introduction to built-in tools.
- Using DuckDuckGo Search for web search.
- Exploring the Shell Tool.
- Creating custom tools using the `@tool` decorator.
- Understanding tool names, descriptions, arguments, and input schemas.
- Creating tools using `StructuredTool`.
- Creating custom tools by inheriting from `BaseTool`.
- Understanding and creating toolkits to organize related tools.

### 2. Tool Calling

**Notebook:** `2_tool_calling_langchain.ipynb`

Explores how language models interact with tools through tool calling.

Topics covered:

- Creating custom tools.
- Binding tools to chat models using `bind_tools()`.
- Understanding how a model generates tool-call requests.
- Inspecting tool calls and their arguments.
- Executing tools and obtaining `ToolMessage` responses.
- Passing tool execution results back to the language model.
- Implementing a manual tool-execution workflow.
- Understanding how multiple tool calls can be handled.

### 3. Currency Conversion Application

**Notebook:** `2.1_currency_conversion_tool_langchain.ipynb`

A practical application of the tool-calling concepts introduced earlier.

The application combines two tools to perform currency conversion:

1. **Conversion Rate Tool:** Retrieves the current exchange rate between two currencies using the ExchangeRate API.
2. **Currency Conversion Tool:** Calculates the converted amount using the retrieved exchange rate.

The notebook explores two implementations:

- **Basic implementation:** The language model is responsible for passing the exchange rate returned by the first tool to the second tool.
- **Application-controlled implementation:** Uses `InjectedToolArg` to prevent the model from directly supplying the conversion rate. Instead, the application retrieves and injects the rate during tool execution.

This demonstrates how multiple tools can work together to solve a practical task and how application-side control can make tool execution more reliable.

### 4. AI Agents

The agent implementations progressively explore how language models can select tools, execute them, observe their results, and use those results to produce responses.

#### 3.0 – Creating a ReAct Agent

**Notebook:** `3.0_agent_langchain.ipynb`

Introduces AI agents using the ReAct (Reasoning and Acting) approach.

Topics covered:

- Understanding the basic idea of AI agents.
- Integrating DuckDuckGo Search as an agent tool.
- Creating a ReAct agent using `create_react_agent` from `langchain_classic.agents`.
- Retrieving and using a ReAct prompt.
- Using `AgentExecutor` to manage the agent's execution loop.
- Invoking the agent and observing its execution.

#### 3.1 – Extending the Agent with Additional Tools

**Notebook:** `3.1_agent_langchain_withupdation.ipynb`

Builds upon the previous agent implementation by introducing an additional custom tool.

Topics covered:

- Creating a custom weather tool using the Weatherstack API.
- Integrating multiple tools into a single agent.
- Combining DuckDuckGo Search and weather information.
- Observing how an agent can select and use different tools to complete a multi-step task.

This demonstrates how an agent's capabilities can be extended by providing it with additional tools.

#### 3.2 – Building Agents Using the New `create_agent()` Interface

**Notebook:** `3.2_agent_langchain_newapproach.ipynb`

Explores the newer agent-building interface introduced in LangChain 1.x.

Topics covered:

- Creating agents using `create_agent()` from `langchain.agents`.
- Providing models, tools, and system prompts.
- Understanding the graph-based execution of agents.
- Invoking agents using the messages-based input format.
- Inspecting intermediate messages and final responses.
- Exploring the use of existing prompt templates with the new interface.

This implementation revisits the earlier agent application using the newer interface and highlights the differences in how agent execution is managed.

## Understanding the Agent Implementation Progression

The three agent notebooks follow a progressive learning path:

| Notebook | Implementation | Execution Management |
|---|---|---|
| 3.0 | ReAct agent with a search tool | `AgentExecutor` |
| 3.1 | ReAct agent with search and weather tools | `AgentExecutor` |
| 3.2 | Agent using `create_agent()` | Internally managed agent graph |

### Legacy Agent Implementation vs. LangChain 1.x

The earlier implementation uses `create_react_agent()` from `langchain_classic.agents` along with `AgentExecutor`.

In this approach, the agent defines the reasoning and tool-selection behavior, while `AgentExecutor` manages the execution loop. It handles the process of obtaining the agent's action, executing the selected tool, returning the observation, and continuing until the agent produces a final response.

The newer `create_agent()` interface in LangChain 1.x provides a different execution framework.

Instead of explicitly wrapping the agent with an `AgentExecutor`, `create_agent()` returns a compiled graph that manages the model and tool execution loop internally.

### Understanding the Agent Graph

An agent graph represents the workflow using connected nodes and edges.

- **Nodes:** Perform individual operations, such as calling the language model or executing tools.
- **Edges:** Define the transitions between nodes.
- **Conditional Edges:** Determine which node should execute next based on the current state or result.

In the agent graph, the model node calls the language model. If the model requests a tool, execution moves to the tool node, which executes the requested tool and returns its result. Control then moves back to the model node. This process continues until the model produces a final response.

### Key Difference

The difference between these implementations is primarily in how the agent's execution workflow is organized and managed.

- **Older implementation:** The execution loop is managed by `AgentExecutor`.
- **Newer implementation:** The execution loop is managed internally by the graph returned by `create_agent()`.

Both approaches can select tools, execute them, observe tool results, and generate responses. Using a graph does not inherently make the language model more intelligent; it provides a structured workflow that can be extended with state management, conditional routing, and other workflow capabilities.

For more information, refer to the official [LangChain Agents documentation](https://docs.langchain.com/oss/python/langchain/agents) and [LangChain v1 migration guide](https://docs.langchain.com/oss/python/migrate/langchain-v1).

## Environment Variables and API Keys

Some notebooks require API keys to access external services.

The following environment variables may be required:

| Environment Variable | Purpose |
|---|---|
| `OPENAI_API_KEY` | Access OpenAI chat models |
| `EXCHANGE_RATE_API_KEY` | Retrieve currency exchange rates |
| `WEATHERSTACK_API_KEY` | Retrieve weather information |

Create a `.env` file in the repository root:

```env
OPENAI_API_KEY=your_openai_api_key
EXCHANGE_RATE_API_KEY=your_exchange_rate_api_key
WEATHERSTACK_API_KEY=your_weatherstack_api_key
```

Load the variables in Python using `python-dotenv`:

```python
import os
from dotenv import load_dotenv

load_dotenv()

openai_api_key = os.getenv("OPENAI_API_KEY")
```

**Important:** Never commit your `.env` file or actual API keys to GitHub. Keep `.env` in `.gitignore` and use `.env.example` to document the required environment variables.

## Further Improvements

Possible areas for extending the repository include:

- Developing more practical applications using multiple tools.
- Exploring additional built-in and custom tools.
- Implementing agents with memory and conversation history.
- Exploring LangGraph for more customized agent workflows.
- Adding human-in-the-loop interactions.
- Building user interfaces for the applications using Streamlit.
- Exploring agent evaluation, tracing, and debugging using LangSmith.

---

**Note:** This repository is intended for learning and experimentation. The notebooks demonstrate individual concepts and practical implementations, and can be extended into more complete applications.
