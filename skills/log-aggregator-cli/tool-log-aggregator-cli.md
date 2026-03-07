# Log Aggregator CLI

## Overview
Aggregate and search through application logs with filtering and real-time streaming

## Installation
```bash
npm install -g log-aggregator-cli
```

## Usage
```bash
log-aggregator-cli --init
log-aggregator-cli --config ./config.json
log-aggregator-cli --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
