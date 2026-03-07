# Environment Sync Tool

## Overview
Sync environment variables across team members and deployment environments securely

## Installation
```bash
npm install -g environment-sync-tool
```

## Usage
```bash
environment-sync-tool --init
environment-sync-tool --config ./config.json
environment-sync-tool --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
