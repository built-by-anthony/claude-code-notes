# Creating your first skill

## Creating a skill

1. create a directory for your skill inside the skills folder The directory name should match the skill name.

```bash
mkdir -p ~./.claude/skills/pr-description
```

2. Create a `SKILL.md` file inside the directory. The file has two parts separated by frontmatter dashes:

```markdown
---
name: pr-description
description: Writes pull request descriptions. Use when creating a PR, writing a PR, or when the user asks to summarize changes for a pull request
---

When writing a PR description:

1. run `git diff main...HEAD` to see all changes on this branch
2. Write a description in the following format:

**What:**
One sentence explaining what this PR does

**Why:**
Brief context on why this change is needed

**Changes:**
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
