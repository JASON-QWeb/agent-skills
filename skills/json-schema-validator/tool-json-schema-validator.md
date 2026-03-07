# JSON Schema Validator

## Overview
Validate JSON data against schemas with detailed error reporting and auto-fix suggestions

## Installation
```bash
npm install -g json-schema-validator
```

## Usage
```bash
json-schema-validator --init
json-schema-validator --config ./config.json
json-schema-validator --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
