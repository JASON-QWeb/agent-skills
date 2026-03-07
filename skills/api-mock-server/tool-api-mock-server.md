# API Mock Server

## Overview
Create mock API servers from OpenAPI specs for frontend development and testing

## Installation
```bash
npm install -g api-mock-server
```

## Usage
```bash
api-mock-server --init
api-mock-server --config ./config.json
api-mock-server --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
