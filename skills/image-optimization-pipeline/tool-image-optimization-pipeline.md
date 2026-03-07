# Image Optimization Pipeline

## Overview
Batch optimize images with WebP/AVIF conversion, resizing, and quality adjustment

## Installation
```bash
npm install -g image-optimization-pipeline
```

## Usage
```bash
image-optimization-pipeline --init
image-optimization-pipeline --config ./config.json
image-optimization-pipeline --output ./dist
```

## Configuration
```json
{
  "preset": "recommended",
  "rules": {},
  "output": "./dist"
}
```
