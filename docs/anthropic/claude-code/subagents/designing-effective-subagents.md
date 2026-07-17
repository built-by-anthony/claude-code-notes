# Designing Effective Subagents 
If you want better control over when a subagent gets triggered automatically, the name and description are what you should tweak. 

The description also plays a second role. When the main agent launches a subagent, it writes an input prompt to kick off the task. It uses the description as guidance for writing this prompt. So the description doesn't just control *when* a subagent runs - it shapes *what then subagent is told to do.*

## Defining an Output Format 
This is the single most important improvement you can make to a subagent is defining an output format in its system prompt. Two things: 
- it creates natural stopping points - the subagent knows it's done when it has filled in each section of the format. 
- it prevents the subagent from runnning too long. Without a defined output, subagents struggle to decide when enough research has been done and tends to run much longer than necessary. 

### Example 

```md
Provide your review in a structure format: 

1. Summary: Brief overview of what you reviewed and overall assessment
2. Critical Issues: Any security vulnerabilities, data integrity risks, or logic errors that must be fixed immediately 
3. Major issues: Quality problems, architecture misalignment, or significant performance concerns 
4. Minor issues: Style inconsistencies, documentation gaps, or minor optimizations
5. Recommendations: Suggestions for improvement, refactoring opportunitites, or best practices to apply. 
6. Approval status: Clear statement of whether code is ready to merge/deploy or requires changes. 
```

## Reporting Obstables 
When a subagent discovers a workaround during its work - like solving a dependeny issue or finding that a certain command needs particular flags - those details need to appear in the summary it returns. 

The kinds of things you want surfaced includes: 
- Setup issues or environment quirks
- Workarounds discovered during the task 
- Commands that needed special flags or configuration 
- Dependencies or imports that caused problems 

Ask for this information in output format: 
```md
Obstables encountered: Report any obstacles encountered during the review process. This can be: setup issues, workarounds disovered or environment quirks. Report commands that needed a special flag or configuration. Report dependencies or imports that cuased problems. 
```

## Limiting Tool Access 
Not every subagent needs access to every tool. Here's how to think about tool access for common subagent types: 
- **Research / read-only subagent** - only needs `Glob`, `Grep` and `Read`. Cannot accidently modify files. 
- **Code Reviewer** - needs `Bash` access to run `git diff` and see what changed, but still doesn't need `Edit` or `Write`. 
- **Styling / code modification agent** - this is where you give `Edit` and `Write` access, because the subagent's job is to actually change your code. 

## Putting It All Together 
Effective subagents share four characteristics: 
1. **Specific descriptions** - the description controls when the subagent is launched and what instructions it receives. Write it to steer both. 
2. **Structured output** - define an output format in the system prompt so the subagent knows when it's done and returns information the main thread can use. 
3. **Obstacle reporting** - include a section in the output format for workarounds, quirks, and problems so the main thread doesn't have to rediscover them. 
4. **Limited tool access** - only give a subagent the tools it actually needs. Read-only for research, bash for reviewers, edit / write only for agents that should change code. 
