# Client review: Larkspur disruption-care agent

**To:** Room 8  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-17 11:08

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. agent.py run_agent(): your diff changed the assistant turn to response.content and the return to text_of(response); readout-trace.json shows 4 API turns.**

The shipped template appended text_of(response) as the assistant message and returned the answer variable. Your diff appends response.content, so tool_use blocks go back to the API. It also returns text_of(response) from the final response. The committed run shows 4 API turns and 4 tool calls against MAX_TOOL_CALLS of 8.

Run python3 run.py K7PQ2M --trace and paste the final answer text with the totals footer.

**2. agent.py search_alternatives: your diff replaced the description "search" with a 441-character one that says it needs only the PNR.**

The new text states the segment, cabin and passenger count are inferred from the booking. It promises up to 7 ranked options, each with an option_id for hold_seat. hold_seat is still 73 characters and send_confirmation is 71. No file shows whether the rewrite changed which tool the model picks.

Run python3 run.py --all --trace and paste the tool-call sequence for each booking shape, so the search_alternatives rewrite has a before and an after.

**3. PITCH.md Number: "13,243 to 17,986 tokens in" for K7PQ2M, but readout-trace.json records 3938 in, 1072 out.**

Your pitch gives the increase from adding next_available_day and fare_rules over MCP. The committed trace shows 3938 tokens in on 4 turns. The trace has no baseline and no MCP-tool run in it. No bench-before or bench-after output sits in the repository, so 13,243 and 17,986 cannot be matched to a run.

Run python3 bench.py --compare on your before and after labels and paste the output, or paste the totals footer that produced each of the two numbers.

**4. agent.py has no cache_control anywhere, and readout-trace.json shows 13424 cache tokens written, 0 read, hit ratio 0.0.**

Your PITCH.md Next says "Turn on prompt caching" and cites cache_read being 0 in all five runs. The trace shows 13424 tokens written to the cache, so some caching is already active on the wire. The static scan finds no cache_control in agent.py. Where those 13424 written tokens come from is not visible in your diff.

Run python3 run.py --tool-tax and paste the output, then say which file sets the cache write.

**5. agent.py tool_list() and PITCH.md Still broken: next_available_day answers for one passenger, and your tool surface now has MCP tools in it.**

Your diff adds mcp_client.tools() to tool_list(), so next_available_day and fare_rules reach the model on every turn. Your own Still broken line says a party of four can be told a day is open when one seat is left. That fault sits in what the tool returns. A larger model gets the same one-passenger answer back. The repository has no evals/cases.json and no case with a multi-passenger booking.

Run python3 run.py --show-tools and paste the next_available_day entry, then add an eval case for a party of four and run python3 eval_harness.py.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (237 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
