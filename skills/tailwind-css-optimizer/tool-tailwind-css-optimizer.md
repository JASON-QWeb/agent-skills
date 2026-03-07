# Tailwind CSS Optimizer

## Overview
Optimize Tailwind CSS output by purging unused classes and minimizing CSS bundle

## Installation
```bash
npm install -g tailwind-css-optimizer
```

## Usage
```bash
tailwind-css-optimizer --init
tailwind-css-optimizer --config ./config.json
tailwind-css-optimizer --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
