# VIBE Coding Security Checklist

> Run this before sharing a link, pushing public code, or connecting real users and real data.

---

## Pre-Ship: 10 Must-Check Items

- [ ] **1. Never expose API keys** — Keep GitHub, OpenAI, Stripe, database URLs, and third-party keys out of frontend code, repos, logs, and AI chat history.
- [ ] **2. Use environment variables and rotate keys** — Store secrets securely, never hardcode them, and replace old or exposed keys. Assume leaked keys are already compromised.
- [ ] **3. Enforce database security** — Use row-level security, least-privileged database roles, private service keys, backups, and server-side checks for sensitive data.
- [ ] **4. Use scoped permissions** — Every key should only have the access it actually needs. Avoid giving full admin permissions by default.
- [ ] **5. Enforce authentication on the backend** — Auth should verify who the user is, not just hide buttons or pages in the UI.
- [ ] **6. Enforce authorization on every sensitive route** — A logged-in user should not access admin routes, private data, or another user's records just by changing a URL.
- [ ] **7. Validate all user input** — Search boxes, prompts, forms, comments, and file uploads can all be manipulated.
- [ ] **8. Use parameterized queries and server-side sanitization** — Never directly trust user input. Prevents injection attacks and data leaks.
- [ ] **9. Add rate limiting** — Limit requests by user or IP to prevent API abuse, scraping, denial-of-service attempts, and cloud bill exhaustion.
- [ ] **10. Use AI to run a security review** — Ask AI to review secrets, auth, input validation, rate limits, error messages, permissions, exposed endpoints, and risky code.

---

## Full Vulnerability Checklist (50 Items)

### Secrets & Credentials
- [ ] 1. Exposed database credentials
- [ ] 2. Public `.env` files
- [ ] 3. Hardcoded API keys
- [ ] 11. Build logs leaking secrets
- [ ] 14. Secrets included in frontend JavaScript
- [ ] 13. Leaked GitHub repos or commit history

### Authentication & Authorization
- [ ] 4. Weak or missing authentication
- [ ] 5. No authorization checks
- [ ] 6. Users able to access other users' data
- [ ] 9. Admin routes left unprotected
- [ ] 15. Client-side-only security checks
- [ ] 24. Broken password reset flows
- [ ] 25. Weak session management
- [ ] 26. JWT secrets that are weak, leaked, or reused
- [ ] 34. API endpoints that trust user-controlled IDs or roles
- [ ] 33. Insecure direct object references (IDOR)

### Database & Storage
- [ ] 7. Open database read/write permissions
- [ ] 8. Misconfigured Firebase / Supabase / S3 buckets
- [ ] 41. Excessive database permissions for the app user

### Input & Injection
- [ ] 16. Missing input validation
- [ ] 17. SQL injection
- [ ] 18. NoSQL injection
- [ ] 21. Insecure file uploads
- [ ] 22. Path traversal bugs

### Frontend & Web
- [ ] 19. Cross-site scripting (XSS)
- [ ] 20. Cross-site request forgery (CSRF)
- [ ] 23. Server-side request forgery (SSRF)
- [ ] 27. Overly permissive CORS
- [ ] 46. Missing security headers
- [ ] 47. Cookies missing `HttpOnly`, `Secure`, or `SameSite`
- [ ] 36. Source maps exposed in production

### API & Infrastructure
- [ ] 28. Rate limits missing on login, signup, APIs, and AI endpoints
- [ ] 29. Public test or staging environments
- [ ] 30. Default credentials left unchanged
- [ ] 31. Webhook endpoints without signature verification
- [ ] 32. Payment or subscription checks only done on the frontend
- [ ] 45. Publicly exposed internal dashboards

### Logging & Monitoring
- [ ] 10. Debug pages exposed in production
- [ ] 12. Verbose error messages leaking stack traces
- [ ] 35. Logs containing tokens, emails, passwords, or private user data
- [ ] 42. No audit logs
- [ ] 43. No monitoring or alerting
- [ ] 44. No backup or restore plan

### Dependencies
- [ ] 37. Dependency vulnerabilities
- [ ] 38. Outdated packages

### AI-Specific
- [ ] 39. Prompt injection in AI features
- [ ] 40. AI tools/actions allowed to access data without permission checks

### Data & Multi-tenancy
- [ ] 48. Unencrypted sensitive data
- [ ] 49. Poor tenant isolation in multi-user apps

### Process
- [ ] 50. Over-trusting generated code without review

---

## Quick AI Security Review Prompt

Paste this into your AI tool of choice before shipping:

```
Review this codebase for security issues. Check for:
- Exposed secrets, API keys, or credentials anywhere in the code
- Missing or bypassable authentication and authorization
- Unvalidated user input and injection vulnerabilities (SQL, NoSQL, XSS, SSRF)
- Insecure file uploads or path traversal risks
- Missing rate limiting on auth and API endpoints
- Overly permissive CORS, database roles, or storage buckets
- Sensitive data in logs, error messages, or frontend bundles
- Missing security headers and insecure cookie settings
- Hardcoded defaults, admin routes without protection
- AI-specific risks: prompt injection, tools with unchecked data access
Report each finding with file, line number, and a one-line fix.
```

---

*Based on VIBE Coding Security Checklist by Jasmine Wong / @cyberjasbytes · itsjasminewong.com*
*50-vulnerability list sourced from: https://www.instagram.com/reels/DWMXQJPgIrx/*
