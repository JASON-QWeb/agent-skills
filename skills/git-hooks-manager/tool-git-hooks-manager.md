# Git Hooks Manager

## Overview
Manage Git hooks with pre-commit, commit-msg, and pre-push automation scripts

## Installation
```bash
npm install -g git-hooks-manager
```

## Usage
```bash
git-hooks-manager --init
git-hooks-manager --config ./config.json
git-hooks-manager --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
