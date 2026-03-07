# Dependency Auditor

## Overview
Audit project dependencies for security vulnerabilities and outdated packages

## Installation
```bash
npm install -g dependency-auditor
```

## Usage
```bash
dependency-auditor --init
dependency-auditor --config ./config.json
dependency-auditor --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
