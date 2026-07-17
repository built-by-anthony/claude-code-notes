# What are skills?

Skills are folders of instructions that Claude Code can discover and use to handle tasks more accurately. Each skill lives in a `SKILL.md` file with a name and description in its frontmatter.
-**Frontmatter**: a block of metadata - usutally written in YAML format - placed at the very top of a document or file.

Claude uses the description to match skills to requests - compares against descriptions and activates against the ones that match.

Skills load on demand - skills activate automatically when Claude recognizes the situation

If you find yourself explaining the same thing to Claude, that is a skill waiting to be written.

## Where Skills Live
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
