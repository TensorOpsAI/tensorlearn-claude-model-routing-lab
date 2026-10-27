# Routing contract
routing.json defines `stages` (extract/reason), `routes:[{taskType,stage}]` and `escalationPolicy`. Stage fields are modelAlias, maxInputTokens, maxOutputTokens and maxRetries. Use Claude Code model aliases such as `haiku`, `sonnet` or `opus`, a different one per stage; full model IDs, token prices and budgets are not part of routing.json.
Nothing in this repository executes routing.json; you try the routing yourself in Claude Code with `/model`. Quality precedes cost: dropping a critical constraint does not earn efficiency credit.
Use source citations in compact handoffs. A statement being repeated many times does not make an obsolete note authoritative. Report actual observed route and usage separately from predicted cost, in your PR description.
