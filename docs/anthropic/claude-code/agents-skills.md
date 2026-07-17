# What are skills? 

Skills are folders of instructions that Claude Code can discover and use to handle tasks more accurately. Each skill lives in a `SKILL.md` file with a name and description in its frontmatter.
-**Frontmatter**: a block of metadata - usutally written in YAML format - placed at the very top of a document or file. 

Claude uses the description to match skills to requests - compares against descriptions and activates against the ones that match. 

Personal skills go in `~/.claude/skills` - global 
Project skills on in `/claude/skills` inside a respository and shared with anyone who clones. 

Skills load on demand - skills activate automatically when Claude recognizes the situation 

If you find yourself explaining the same thing to Claude, that is a skill waiting to be written. 

## Skills example - grilling skill -> SKILL.md 
### Skills Frontmatter example: 
---
name: grilling
description: Grill the user relentlessly about a plan, decision, or idea. Use when the user wants to stress-test their thinking, or uses and `grill` trigger phrases. 
--- 

## Skills Body example: 
Interview me relentlessly about every aspect of this until we reach a shared understanding. Walk down each branch of the decision tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer. 

Ask the questions one at a time witing for feedback on each question before continuing. Asking multiple questions at once is bewildering. 

If a *fact* can be found by exploring the environment (filesystem, tools, etc.), look it up rather than asking me. The *decisions*, though are mine - put each one to me and wait for my answer.

Do not act on it until I confirm we have reached a shared understanding. 

#### Where Skills Live 
- **Personal Skills**: go in `~/.claude/skills` (your home directory) - these are global 
- **Project skills**: go in `.claude/skills` inside the root directory of your repository - anyone who clones this repo gets the skills automatically. 

## Skills vs. CLAUDE.md vs. Slash commands 
- CLAUDE.md - files load into every conversation. 
- Skills - Load on demand when they match your request, only loads the name and description initially, so they don't fill up your context window. 
- Slash commands - require you to explicitly type them. Skills don't. 

## When to use skills 
- Code review standards your team follows. 
- Commit message formats you prefer. 
- Brand guidelines for your organization. 
- Documentation templates for sepcific types of docs 
- Debugging frameworks for particular frameworks. 

Rule of thumb: if you find yourself explaining the same thing to Claude repeatedly, that's a skills waiting to be written. 

# Creating your first skill 
## Creating a skill 

1. create a directory for your skill inside the skills folder The directory name should match the skill name. 

```bash
mkdir -p ~./.claude/skills/pr-description
``` 

2. Create a `SKILL.md` file inside the directory. Th file has two parts separated by frontmatter dashes: 

```md
--- 
name: pr-description
description: Writes pull request descriptions. Use when creating a PR, writing a PR, or when the user asks to summarize changes for a pull request
--- 

When writing a PR description: 

1. run `git diff main...HEAD` to see al changes on this branch
2. Write a description in the following format: 

What: 
one senetence explaining what this PR does 

Why: 
Breif context on why this change is needed 

Changes: 
- Bullet points of specific changes made 
- Group related changes together 
- Mention any files deleted or removed 
```

- **name** identifies your skill 
- **description** tells Claude when to use it

**Note:** Claude Code loads skills at startup, so restart your session after creating one. You can verify by checking. 

## How Skill Matching Works 
When Claude Code starts it scans four locations for skills and **only loads the name and description**. When you send a request, Claude compares your message against the description of all available skills. 

These are prioritized. 
Enterprise -> Personal -> Project -> Plugins 

# Configuraiton and multi-file skills 

## Key takeaways 
- `name` and `description` are required - `allowed-tools` and `model` are optional but powerful additions. 
- A good description answers two questions: What does the skill do? When should Claude use it? 
- `allowed-tools` restricts which tools Claude can use when the skill is active - useful for read-only or security-sensitive workflows. 
- **Progressive disclosure:** keep `SKILL.md` under 500 lines and link to supporting files (references, scripts, assets) that Claude reads only when needed. 
- **Script execute without loading their contents into context** - only the output consumes tokens, keeping context efficient. 

## Skill Metadata fields 
- **name** (required) - Identifies your skill. User lowercase letters, numbers, and hyphens only. Maximum 64 characters. Should match your directory name. 
- **description** (required) - Tells Claude when to use the skill. Maximum 1,024 characters. Most important, Claude uses for matching. 
- **allowed-tools** (optional) - Restricts which tools Claude can use when the skill is active. 
- **model** (optional) - Specific which Claude model to use for the skill. 

## Example of `allowed-tools`

```md
---
name: codebase-onboarding 
description: Helps new developers understand how the codebase works 
---
```

## Progressive Discolsure 
Keep essential instructions in `SKILL.md` and put detailed reference material in separate files that Claude reads only when needed. 

The open standard suggests organization as follows: 
- `scripts/` - Executable code 
- `references/` - Additional documentation 
- `assets/` - Images, templates, or other data files 

Then in `SKILL.md`, link to the supporting files with clear instructions about when to lead them.

A good rule of thumb is to **keep `SKILL.md` under 500 lines.** If you're exceeding that, consider whether the content should be split into separate reference files. 

## Using Scripts Efficiently 
The key instruction to include in your `SKILL.md` is to tell claude to *run* the script, not *read* it. 

This is particularly useful for: 
- Environment validation
- Data transformations that need to be consistent 
- Operations that are more reliable as tested code than geenrated code
