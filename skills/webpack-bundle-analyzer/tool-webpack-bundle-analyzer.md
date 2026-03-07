# Webpack Bundle Analyzer

## Overview
Analyze webpack bundles to identify large dependencies and optimize bundle size

## Installation
```bash
npm install -g webpack-bundle-analyzer
```

## Usage
```bash
webpack-bundle-analyzer --init
webpack-bundle-analyzer --config ./config.json
webpack-bundle-analyzer --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
