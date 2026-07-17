# AI Learning Notes

A personal knowledge base for AI tools and concepts, organized by vendor and topic.

## Quick Start

### Prerequisites
- Python 3.7+

### Installation

Create and activate a virtual environment:
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

Install dependencies:
```bash
pip install -r requirements.txt
```

### Running Locally
```bash
mkdocs serve
```

Then visit `http://localhost:8000` in your browser.

## Structure

- **Homepage** — Overview of all topics
- **Anthropic** — Claude and related tools
  - **Claude Code** — Claude Code features and concepts
    - Agents & Skills
    - *(More topics to come)*

## Adding New Topics

1. Create a `.md` file in the appropriate category folder under `docs/`
2. Add the page to the navigation in `mkdocs.yml`
3. Run `mkdocs serve` to preview locally

Example: Adding a new Claude Code topic called "Prompt Caching":
```yaml
nav:
  - Home: index.md
  - Anthropic:
    - Claude Code:
      - Agents & Skills: anthropic/claude-code/agents-skills.md
      - Prompt Caching: anthropic/claude-code/prompt-caching.md
```

## Deployment

Currently local-only. To deploy to GitHub Pages in the future, run:
```bash
mkdocs gh-deploy
```
