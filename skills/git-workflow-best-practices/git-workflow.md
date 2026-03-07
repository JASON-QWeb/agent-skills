# Git Workflow Best Practices

## Description
Professional Git workflow patterns including branching strategies, commit conventions, and collaboration techniques for team development.

## Branching Strategy
### Git Flow
- `main` - production-ready code
- `develop` - integration branch
- `feature/*` - new features
- `hotfix/*` - emergency fixes
- `release/*` - release preparation

### Commit Convention
```
<type>(<scope>): <subject>

Types: feat, fix, docs, style, refactor, test, chore
```

## Essential Commands
```bash
# Interactive rebase for clean history
git rebase -i HEAD~5

# Stash with message
git stash push -m "WIP: feature X"

# Cherry-pick specific commits
git cherry-pick abc123

# Bisect to find bugs
git bisect start
git bisect bad HEAD
git bisect good v1.0.0
```

## Best Practices
1. Write meaningful commit messages
2. Keep commits atomic and focused
3. Rebase feature branches before merging
4. Use pull requests for code review
5. Never force push to shared branches
