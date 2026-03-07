# Docker Deployment Skill

## Description
Complete Docker deployment workflow covering multi-stage builds, Docker Compose orchestration, and production best practices.

## Multi-Stage Build
```dockerfile
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

# Production stage
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
EXPOSE 3000
CMD ["node", "dist/server.js"]
```

## Docker Compose
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://db:5432/app
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:16-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: app
      POSTGRES_PASSWORD: secret

volumes:
  pgdata:
```

## Best Practices
1. Use specific image tags, not `latest`
2. Minimize layer count and image size
3. Run as non-root user
4. Use health checks
5. Scan images for vulnerabilities
