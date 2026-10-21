# Agentic AI with LangGraph

Notebooks from learning LangGraph, from a basic workflow to LLM-powered chains.

## Notebooks

| Notebook | What it does |
|---|---|
| `0_test_installation.ipynb` | Checks that the environment and packages are installed correctly. |
| `1_bmi_workflow.ipynb` | First workflow, with no LLM. Defines the state (`TypedDict`), adds nodes, connects edges, compiles and runs. Calculates BMI and labels the category: `START -> calculate_bmi -> label_bmi -> END`. |
| `02_llm_workflow.ipynb` | Single-node workflow that sends a question to a Claude model and stores the answer in the state. |
| `3_prompt_chaining.ipynb` | Prompt chaining. Turns a topic into a blog title, outline and full post, then evaluates it: `generate_title -> create_outline -> create_content -> evaluate_content`. |
| `4_parallel_workflow1.ipynb` | Parallel workflow, with no LLM. Calculates a batsman's strike rate, balls per boundary and boundary percentage in parallel, then summarizes. Nodes return only the keys they update, to avoid `InvalidUpdateError`. |
| `5_parallel_workflow2.ipynb` | Parallel LLM workflow. Three nodes evaluate an essay (language, analysis, clarity) at the same time using structured output (`EvaluationSchema`), then a final node writes overall feedback and the average score. |
| `6_conditional_workflow1.ipynb` | Simple conditional workflow. A routing function sends a number to `even_node` or `odd_node`. |
| `7_conditional_workflow2.ipynb` | Data engineering conditional workflow. Profiles a batch's null percentage, then routes it to load, clean then load, or quarantine and alert. |
| `8_iterative_workflow.ipynb` | Iterative (loop) workflow. A generator writes a tweet, an evaluator (structured output, `approved` or `needs_improvement`) judges it, and an optimizer rewrites it until approved or `max_iteration` is reached. Keeps `tweet_history` and `feedback_history` with `operator.add` reducers. |
| `9_basic_chatbot.ipynb` | Basic chatbot. Conversation history lives in `messages` (using the `add_messages` reducer), and a `MemorySaver` checkpointer with a `thread_id` gives each chat its own memory. Includes a terminal chat loop. |
| `10_persistent_chatbot1.ipynb` | Persistent chatbot. Swaps `MemorySaver` for a database-backed `SqliteSaver`, so conversations survive a restart. Shows per-user `thread_id`s, reading stored history, listing threads, and moving to `PostgresSaver` for production. |
| `10_persistent_chatbot2.ipynb` | Checkpointer demo with the joke and explanation workflow (`generate_joke -> generate_explanation`) compiled with `InMemorySaver` and run under a `thread_id`. Uses `.text` instead of `.content` so thinking blocks don't end up in the state. |

## Concepts covered
- State as a `TypedDict`
- Nodes as functions that read and update the state
- `StateGraph`, `add_node`, `add_edge`, `compile`, `invoke`
- Visualizing the graph with `draw_mermaid_png()`
- Calling an LLM (`ChatAnthropic`) inside a node
- Chaining LLM calls so one node's output feeds the next
- Parallel branches, and returning partial state updates from nodes
- Reducers (`Annotated` keys) for combining results from parallel nodes
- Structured output with Pydantic (`with_structured_output`)
- Conditional routing with `add_conditional_edges`
- Loops: routing back to an earlier node until a condition is met
- Chat state with the `add_messages` reducer
- Checkpointers (`MemorySaver`, `InMemorySaver`, `SqliteSaver`) and `thread_id` for persistent memory
- Using `response.text` instead of `response.content` to get plain text from Claude models that return content blocks

## Setup
1. Create and activate a virtual environment.
2. Install: `pip install langgraph langchain-anthropic python-dotenv`. The SQLite chatbot (notebook 10_persistent_chatbot1) also needs `langgraph-checkpoint-sqlite`.
3. Create a `.env` file with `ANTHROPIC_API_KEY=your_key`. It is git-ignored, so don't commit it.
