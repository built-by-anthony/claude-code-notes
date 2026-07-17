# Creating a subagent 

You can create your own custom subagents that specialize in specific tasks  - like reviewing codes, writing tests, or checking documentation. They are defined as markdown files wwith YAML frontmatter that tell Claude when to use the subagent and how the subagent should behave. 

## The Config File 
The subagent config file is saved to your project, typically you ask Claude to create this or you can manually create it here `.claude/agents/your-agent-name.md`

## System Prompts 
The body of the markdown file (everything below the YAML frontmatter) is the system prompt. This is where you give the subagent its instruction: what it should focus on, how it should analyze things, and how it should report its findings back to the main agent. 

A well written system prompt is the difference between a useful subagent and one that misses the point. Be specific about what the subagent should look for and how it should structure its output. 

### Example: 
```md
---
name: code-quality-reviewr 
description: Use this agent when you need to review recently written or changed code. 
tools: Bash, Glob, Read, WebFetch, WebSearch
model: sonnet 
color: purple

You are an expert code reviewer specializing in quality assurance, security, and aherence to project standard. Your role it to thoroughly examine recent changes and identify issues that could impact relability, security, maintainability, etc. 
```

- `name` - a unique identifer for the subagent. This is how you reference it, either by asking Claude directly or by typing `@agent code-quality-reviewer` in your message. 
- `description` - controls when Claude decides to use the subagent. This must be a single line (use escaped newline characters `\n` if you need breaks. 
- `tools` - list which tools the subagent can access. This matches whatver you selected during generation, but you can edit the list here at any time. 
- `model` - specifies which Claude model to use: (`sonnet`, `opus`, `haiku`, or `inherit`).
- `color` - the UI color for identifying the subagent.


