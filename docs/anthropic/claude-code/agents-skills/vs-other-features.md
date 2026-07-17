# Skills vs. other Claude Code features

## Key Takeaways
- **CLAUDE.md** loads into every conversation, best for always-on project standards -> **Skills** load on demand, good for specific tasks
- **Subagents** run in isolated exeuction contexts, delegated work -> **Skills** add knowledge to your current conversation
- **Hooks** are event driven (fire on save, tool calls) -> **Skills** are request driven (activate based on what you are asking)
- **MCP servers** provide external integrations - a different category entirely from skills.
- Each feature handles its own specialty - **combine them** rather than forcing everyting into one approac.

## Putting it all together
- **CLAUDE.md** - always-on project standards
- **Skills** - task-specific expertise that loads on demand
- **Hooks** - automated operations triggered by events
- **Subagents** - isolated execution contexts for delegated work
- **MCP servers** - external tools and integrations

Each handles its own specialty.

Use skills when you have knowledge that Claude should apply automatically when the topic is relevant and, and combine them with other features for comprehensive customization.

## Skills and subagents
Subagents don't automatically see your skills.

There are some important distictions to understand:
- **Built-in agents** (like Explorer, Plan, and Verify) can't access skills at all.
- **Custom  subagents** you define *can* use skills, but only when you explicity list them.
- Skills are loaded when the subagent starts, not on demand like in the main conversation.

To create a custom subagent with skills, add an agent markdown file in `.claude/agents`

### Agent file example

```md
name: frontend-security-accessibility-reviewer
description: "Use this agent when you need to review frontend code for accessibility"
tools: Bash, Glob, Grep, Read, WebFetch, WebSearch, Skill...
model: sonnet
color: blue
skills: accessibility-audit, performance-check
```

Argument definitions: 

- `name`: unique identifier for the subagent (lowercase letters and hyphens). Claude uses this to recognizw when to delegate this to an agent. 
- `description`: When Claude should use this subagent. Guides Claude's decision to delegate. 
- `tools`: Which tools the subagent can access. If omitted, it inherits all tools from the main conversation. 
- `model`: Which Claude model to use for this subagent (`sonnet`, `opus`, `haiku`). If omitted, it inherits the main conversation's model. 
- `color`: Visual indicator in the UI to distinguish this subagent from others. 
- `skill`: Skills to preload into the subagent's context so it can use them without being asked.
