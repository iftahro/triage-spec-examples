# Answer key: flawed spec critique (instructor only)

| # | Problem | Category | What the agent must guess / risk |
|---|---|---|---|
| R1 | Req 1 "figure out what they are about" | Ambiguity, Incompleteness | Agent has to guess what "figure out what they are about" means; it can scan code or other excessive stuff |
| R2 | Req 2 "the right category (bug, feature, docs, etc.)" | Untestability, Incompleteness | Agent has to guess the categories; risk is it will invent many and call the same category by two different names |
| R3 | Req 3 "Severity should be determined accurately" | Untestability, Incompleteness | Agent has to guess the severity levels (1-5? low/high?) and what "accurately" means; risk is the levels don't match the routing rules and there's no way to check quality |
| R4 | Req 4 "Important issues must be escalated quickly" | Ambiguity, Untestability | Agent has to guess what "important issues" (and "quickly") means; risk is that really important issues won't be treated as such |
| R5 | Req 5 "output the queue, SLA and whether to escalate" | Incompleteness | Agent has to guess the available queues; it can invent queues that don't exist |
| R6 | Req 5 vs Req 7: who decides the queue | Inconsistency, Design-in-requirements | Agent has to guess who decides the queue: the model (req 5) or fixed rules (req 7)? Risk is routing becomes random and untestable, and a malicious issue can talk the model into a queue |
| R7 | Req 6 "If the AI isn't sure, it should do its best" | Ambiguity, Untestability | Agent has to guess what "do its best" means; risk is that low-confidence issues will disappear |
| R8 | Req 7: critical bug with no repro steps | Inconsistency | Agent has to guess which rule wins when a bug is critical AND has no repro steps: clarify queue or on-call queue? Risk is a real outage waits in a clarification queue |
| R9 | Req 8 "fast" | Missing non-functional concern, Untestability | Agent has to guess what "fast" means; risk is that it will prioritize speed over robustness |
| R10 | Req 8 "secure" | Missing non-functional concern, Untestability | Agent has to guess what "secure" means; risk is it can lower our security requirements and run malicious commands from the issue data |
| R11 | Req 9 "Use the issue's labels and comments to improve accuracy" | Untestability, Incompleteness | Agent has to guess what "improve accuracy" is; risk is existing labels often already contain the answer, so the AI looks accurate in testing but is just copying |
| R12 | Req 10 "Confidence should be between 0 and 100" | Ambiguity | Agent has to guess what "confidence" means: the AI coding agent's confidence or the triage result's? Whole number or decimal? What to do with values like 150? |
| R13 | US-A "so that things are better" | Incompleteness, Untestability | Agent has to guess what "things are better" means; risk is that its "better" doesn't correlate with our "better" |
| R14 | US-B "I want the AI to route issues" | Ambiguity, Incompleteness | Agent has to guess what it means for the AI to route; risk is that the AI will run commands with issue data |
| R15 | US-C "GPT-4 with temperature 0 and a regex parser" | Design-in-requirements | Dictates how to build it (GPT-4, temperature 0, regex) instead of what the user needs; agent has to guess what "output is reliable" means; risk is it will hand unreliable output forward |
| R16 | US-D "handle weird issues gracefully" | Ambiguity | Agent has to guess what "weird issues" and "gracefully" mean; risk is that it will downgrade real weird issues and handle them too gracefully |

## Requirement topics that are completely missing

1. Malicious issue data (security threat model): issue text is written by strangers and can contain malicious commands or prompt injection; nothing says it must be treated as untrusted data
2. SLA values: SLA is mentioned but the actual deadlines (hours per severity) are never defined
3. Failure handling: no policy for invalid or broken AI output (retry? how many times? where does the issue go so it isn't lost?)
