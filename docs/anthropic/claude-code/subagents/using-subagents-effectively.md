# Using Subagents Effectively

## When Subagents Shine 
Subagents work best when the exploration is separate from the execution. If each step in a task depends on what the previous step discovered, you want that work in your main thread. But if you just need an answer and don't care about the journey, delegate it. 

Subagents excel at tasks where: 
- You need a result, not a play-by-play of how it was found 
- The exploratory work would clutter your main thread's context
- The task benefits from a fresh perspective or a custom system prompt

### Research Tasks 
Classic example, a research agent can read dozens of files, trace through function calls, and explore different code paths. All that exploration stays in the subagents context. Your main thread receives a clean summary. 

Code reviews are another example of this. 

## When Subagents Hurt 
Three common anti-patterns to watch out for: 
1. `Expert claims` - these add no value becuase Claude already has this knowledge. 
2. `Sequential pipelines` - Pipelines work when tasks are truly independent. They fail when each step depends on discoveries from from the previous step. Information gets lost in the handoff between agents. 
3. `Test runners` - Test runner subagents tend to hide the information you need. Test runner could return "test failed" without enough detailed information to debug.  

## The Decision Rule 
Ask yourself one question **does the intermediat work matter?** 
- if not, delegate to subagent. 
- if yes, keep in main thread. 

### Use Subagents for 
- Research and exploration 
- Code reviews 
- Tasks that need a custom system prompt 

### Avoid Subagents for 
- "Expert" personas that don't add real capability 
- Multi-step pipelines where each step depends on the last 
- Running tests where you need full output for debugging 

