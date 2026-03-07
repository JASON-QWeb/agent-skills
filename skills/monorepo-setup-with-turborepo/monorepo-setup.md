# Monorepo Setup with Turborepo

## Description
Setting up and managing a monorepo using Turborepo with shared packages, workspaces, and optimized build pipelines.

## Project Structure
```
my-monorepo/
├── apps/
│   ├── web/          # Next.js app
│   ├── mobile/       # React Native app
│   └── api/          # Express server
├── packages/
│   ├── ui/           # Shared component library
│   ├── utils/        # Shared utilities
│   └── config/       # Shared configs (ESLint, TS)
├── turbo.json
└── package.json
```

## Turbo Configuration
```json
{
  "$schema": "https://turbo.build/schema.json",
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": ["dist/**", ".next/**"]
    },
    "test": {
      "dependsOn": ["build"]
    },
    "dev": {
      "cache": false,
      "persistent": true
    }
  }
}
```

## Shared Package
```json
{
  "name": "@repo/ui",
  "main": "./src/index.ts",
  "types": "./src/index.ts",
  "scripts": {
    "build": "tsup src/index.ts --format esm,cjs --dts"
  }
}
```

## Key Commands
```bash
turbo run build          # Build all packages
turbo run dev --filter=web  # Dev only web app
turbo run test --parallel   # Test in parallel
```
