# What are Subagents?

Subagents are specialized that Claude Code can delegate tasks to. Think of them as focused helpers: each one runs its own conversation context window, does it work, and returns a summary to the main thread. The intermediate steps - all the file reads, searches, and tool calls - stay isolated and never clutter your main conversation.

## Key Takeaways 
- They break work into focused pieces, letting each subagent  concentrate on a specific task 
- They keep your main context window clean by isolating all the intermediate work. 
- They bring back just the information you need as a concise summary
## Why Subagents Mattter 
Context fills up (think the model gets dumber as the context window fills up). 

Subagents solve this by spinning up a separate context window. The subagent recieves two things: 
- **A custom system prompt** from your configuration file that defines the subagent's role and behavior. 
- **A task description** written by the parent agent based on what you asked for. 

The subagent then works on its own. When it's done only a summary comes back to your main conversation. The entire subagent conversation is then discarded. 

This means your **context stays clean**

## Built-in Subagents 
- **General purpose subagent** - for multi-step tasks that require both exploration and action
- **Explore** - for fast searching and navigation of codebases
- **Plan** - used during plan mode for research and analysis of your codebase before presenting a plan

## Custom Subagents 
You can create your own subagents with custom system prompts and tool access. This lets you define specialized agents tailored to your workflow. Code reviewer, test writer, docmentation generator, anything else you need. 


