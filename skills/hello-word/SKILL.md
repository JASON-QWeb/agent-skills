---
name: hello-world
description: A minimal example skill that demonstrates the agent skill format. Use this as a template when creating new skills. Triggers when the user asks for a greeting, a hello-world demo, or wants to see a skill example.
---

# Hello World Skill

## test update

A minimal skill to demonstrate the agent skills format.

## Usage

When triggered, greet the user warmly and explain that this is a demo skill.

### Example Response

> 👋 Hello! This is the **hello-world** skill in action.
> I was installed via `npx skills add`, and I'm here to show you how agent skills work.

## Creating Your Own Skill

A skill only needs a `SKILL.md` file with:

1. **YAML frontmatter** — `name` and `description` (used for discovery and triggering)
2. **Markdown body** — instructions the agent follows when the skill is activated

Optional directories: `scripts/`, `references/`, `assets/`

That's it. Put it in a GitHub repo under a `skills/` folder and anyone can install it with:

```bash
npx skills add owner/repo
```
