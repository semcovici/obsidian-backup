
## Overwiew
LangGraph is a library for building stateful, multi-actor applications with LLMs, used to create agent and multi-agent workflows. Compared to other LLM frameworks, it offers these core benefits: cycles, controllability, and persistence. LangGraph allows you to define flows that involve cycles, essential for most agentic architectures, differentiating it from [[DAG-based solutions]]. As a very low-level framework, it provides fine-grained control over both the flow and state of your application, crucial for creating reliable agents. Additionally, LangGraph includes built-in persistence, enabling advanced human-in-the-loop and memory features.

LangGraph is inspired by [Pregel](https://research.google/pubs/pub37252/) and [Apache Beam](https://beam.apache.org/). The public interface draws inspiration from [NetworkX](https://networkx.org/documentation/latest/). LangGraph is built by LangChain Inc, the creators of LangChain, but can be used without LangChain.

## Key Features[¶](https://langchain-ai.github.io/langgraph/#key-features "Permanent link")

- **Cycles and Branching**: Implement loops and conditionals in your apps.
- **Persistence**: Automatically save state after each step in the graph. Pause and resume the graph execution at any point to support error recovery, human-in-the-loop workflows, time travel and more.
- **Human-in-the-Loop**: Interrupt graph execution to approve or edit next action planned by the agent.
- **Streaming Support**: Stream outputs as they are produced by each node (including token streaming).
- **Integration with LangChain**: LangGraph integrates seamlessly with [[LangChain]] and [[LangSmith]] (but does not require them).

## Resources
oficial website: [LangGraph](https://www.langchain.com/langgraph)
LangChain Academy Course: [Introduction to LangGraph](https://academy.langchain.com/courses/intro-to-langgraph "https://academy.langchain.com/courses/intro-to-langgraph")
PT-BR video with the basics: [Começando com LangGraph - tutorial com exemplos](https://www.youtube.com/watch?v=ni4llX24OAk)