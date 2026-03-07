# Web Security Checklist

## Description
Essential web application security checklist covering OWASP Top 10, authentication, and data protection.

## Authentication
- [x] Use bcrypt/argon2 for password hashing
- [x] Implement rate limiting on login endpoints
- [x] Use secure session management
- [x] Enable MFA where possible

## Input Validation
```javascript
// Always validate and sanitize
const sanitized = DOMPurify.sanitize(userInput)

// Use parameterized queries
const user = await db.query(
  'SELECT * FROM users WHERE id = $1',
  [userId]
)
```

## HTTP Security Headers
```
Content-Security-Policy: default-src 'self'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Strict-Transport-Security: max-age=31536000
X-XSS-Protection: 1; mode=block
```

## CORS Configuration
```javascript
app.use(cors({
  origin: ['https://yourdomain.com'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  credentials: true
}))
```

## Data Protection
1. Encrypt sensitive data at rest
2. Use TLS 1.3 for data in transit
3. Implement proper access controls
4. Log security events
5. Regular dependency audits
