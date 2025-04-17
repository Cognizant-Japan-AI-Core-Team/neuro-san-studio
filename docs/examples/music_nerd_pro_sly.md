# Music Nerd Pro Sly

This simple agent network consists in a frontman agent and a "tool" agent,
i.e. an agent that calls Python code.
This is a good way to get familiar with coded tools and `sly_data to carry a state.
It allows to test for:
- deterministic answers
- follow-up questions
- calling a coded tool (a Python function)
- using `sly_data` to keep track of a variable.

## File

[music_nerd_pro_sly.hocon](../../registries/music_nerd_pro_sly.hocon)


## Description

Music nerd Pro is an agent network that can answer questions about music since the 60s.
It also calls a tool that increments a counter of the number of questions answered.
The agent knows it has to call the tool to keep track of the `running cost`, but it
has no idea how the cost is calculated. Instead of asking the LLM to figure out the
current `running cost` and pass it down to the Accountant tool,
like in `music_nerd_pro`, the Accountant tool uses a `running_cost` variable
in the `sly_data` to keep track of the cost.

## Example conversation:

```
Human: Which band wrote Yellow Submarine?
AI: ... The Beatles ...
    ... running cost ... $1.00 ...
```
Expectation: the answer should contain:
- "The Beatles".
- a running cost of $1.00.

Follow-up question, to check the conversation history is carried over:
```
Human: Where are they from?
AI: ... Liverpool ...
    ... running cost ... $2.00 ...
```
The answer should contain "Liverpool".
And a running cost of $2.00.
Debug logs should show that the agent has passed the previous cost to the tool.
