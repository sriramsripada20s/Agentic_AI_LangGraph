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

## Setup
1. Create and activate a virtual environment.
2. Install: `pip install langgraph langchain-anthropic python-dotenv`
3. Create a `.env` file with `ANTHROPIC_API_KEY=your_key`. It is git-ignored, so don't commit it.
