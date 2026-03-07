# Code Coverage Reporter

## Overview
Generate code coverage reports with visual diffs and trend tracking across commits

## Installation
```bash
npm install -g code-coverage-reporter
```

## Usage
```bash
code-coverage-reporter --init
code-coverage-reporter --config ./config.json
code-coverage-reporter --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
