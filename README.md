# Agent Skills & Rules

Example skills and rules for testing [skillsandruless](https://www.npmjs.com/package/skillsandruless).

## Skills

| Skill | Description |
| --- | --- |
| [code-reviewer](skills/code-reviewer/) | Review code for bugs, security issues, and best practices |
| [git-commit-helper](skills/git-commit-helper/) | Generate clear conventional commit messages |
| [api-designer](skills/api-designer/) | Design clean RESTful APIs |

## Rules

| Rule | Description |
| --- | --- |
| [typescript](rules/typescript.md) | TypeScript coding standards |
| [react](rules/react.md) | React component best practices |
| [security](rules/security.md) | Application security guidelines |

## Usage

```bash
# Install all skills
npx skillsandruless add JASON-QWeb/agent-skills

# Install all rules
npx skillsandruless add JASON-QWeb/agent-skills --rule

# Install a specific skill
npx skillsandruless add JASON-QWeb/agent-skills --skill code-reviewer

# Install a specific rule
npx skillsandruless add JASON-QWeb/agent-skills --rule --skill react
```
