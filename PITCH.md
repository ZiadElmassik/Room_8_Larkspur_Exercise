# PITCH.md

Six lines and a lever. Your words. The last two are scored.

Built: A support agent for disrupted Larkspur flights, with Larkspur's nine tools plus next_available_day and fare_rules served over MCP.
Does: It finds the booking, checks the flight's real status, checks what the policy says the customer is owed, finds the earliest day with a free seat, and offers flights to rebook onto.
Number: 13,243 to 17,986 tokens in, for one ticket (K7PQ2M), after adding the two MCP tools.
Safety check: It never books a seat on its own. confirm_rebooking needs a token that only the customer's own Confirm click creates.
Next: Turn on prompt caching. Every run re-sends the same instructions and tool descriptions, and cache_read is 0 in all five runs.
Still broken: next_available_day only answers for one passenger, so a party of four can be told a day is open when only one seat is left.
Lever: <cost | speed | intelligence>

## Priya asked

Costs:
Wrong:
Runs it:
Left out:
