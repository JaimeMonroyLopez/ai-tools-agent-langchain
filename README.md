# AI Agent with Tools (LangChain)

An AI agent that **decides by itself** which tool to use to answer a question: a calculator, a search tool, or both.

## What does it do?

```
"What is 23 * 5?"                  →  Calculator          →  115
"What is the capital of France?"   →  Search              →  Paris
"Add 34 and search India's pop."   →  Calculator + Search →  149 and 1,428,627,663
"Multiply my first result by 2"    →  Memory + Calculator →  230
```

## How does it work?

1. The user asks a question.
2. The agent **thinks**: *"Do I need a tool?"*
3. If so, it **picks a tool** and uses it.
4. It **reads the result** and decides whether it needs another tool.
5. When it has everything, it **answers**.

This loop is called **ReAct** (Reason + Act), and you can see every step in the notebook:

```
Thought: Do I need to use a tool? Yes
Action: Calculator
Action Input: 23 * 5
Observation: 115
AI: 23 * 5 = 115
```

## Key concepts

| Concept | In simple words |
|---|---|
| **Tool** | A Python function the agent can use. Its *description* tells the agent when to use it. |
| **Prompt template** | The agent's instructions, e.g. "never do math in your head, use the Calculator". |
| **Memory** | Remembers the conversation, so "my first result" makes sense. |
| **Agent** | The LLM plus the tools plus the loop that connects them. |

## How to run it

```bash
pip install -r requirements.txt
set GOOGLE_API_KEY=your-key        # free key: https://aistudio.google.com/apikey
jupyter notebook langchain_tools_agent.ipynb
```

## Files

- `langchain_tools_agent.ipynb`: the agent, with real outputs
- `langchain_tools_agent.html`: the same notebook, viewable in a browser
- `submission.html`: my written explanation (tools, prompt strategy, reasoning, sample outputs)

## What I learned

- **Clear rules work better than vague ones.** Without "never do math in your head", the model skips the calculator.
- **Check the steps, not just the answer.** At first the model *said* it used Search, but the tool never ran. I added a small parser that forces the real tool call.
- **Never use `eval()` blindly.** The calculator only allows numbers and math operators.
- **The model is replaceable.** I used Gemini; switching to OpenAI is one line of code.
