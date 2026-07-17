# Configuration and multi-file skills

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

```yaml
---
name: codebase-onboarding
description: Helps new developers understand how the codebase works
allowed-tools:
  - Read
  - Bash
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
