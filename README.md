# Agentic AI with LangGraph

Notebooks from learning LangGraph, from a basic workflow to LLM-powered chains.

## Notebooks

| Notebook | What it does |
|---|---|
| `0_test_installation.ipynb` | Checks that the environment and packages are installed correctly. |
| `1_bmi_workflow.ipynb` | First workflow, with no LLM. Defines the state (`TypedDict`), adds nodes, connects edges, compiles and runs. Calculates BMI and labels the category: `START -> calculate_bmi -> label_bmi -> END`. |
| `02_llm_workflow.ipynb` | Single-node workflow that sends a question to a Claude model and stores the answer in the state. |
| `3_prompt_chaining.ipynb` | Prompt chaining. Turns a topic into a blog title, outline and full post, then evaluates it: `generate_title -> create_outline -> create_content -> evaluate_content`. |

## Concepts covered
- State as a `TypedDict`
- Nodes as functions that read and update the state
- `StateGraph`, `add_node`, `add_edge`, `compile`, `invoke`
- Visualizing the graph with `draw_mermaid_png()`
- Calling an LLM (`ChatAnthropic`) inside a node
- Chaining LLM calls so one node's output feeds the next

## Setup
1. Create and activate a virtual environment.
2. Install: `pip install langgraph langchain-anthropic python-dotenv`
3. Create a `.env` file with `ANTHROPIC_API_KEY=your_key`. It is git-ignored, so don't commit it.
