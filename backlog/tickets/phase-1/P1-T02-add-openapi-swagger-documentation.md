# P1-T02: Add OpenAPI/Swagger Documentation

**Phase:** 1 - Foundation
**Week:** 1 - Content Completion
**Priority:** High
**Effort:** 4 hours
**Status:** Not Started

---

## Objective

Create comprehensive documentation for OpenAPI Specification and Swagger tooling to resolve 9 TODO references across RESTful API design pages.

## Context

Multiple pages reference OpenAPI/Swagger but the content doesn't exist:
- `restful-api-design.md` - 6 TODOs
- `api-design-principles.md` - 3 TODOs

This is essential for completing the Web Services & API Design section.

## Success Criteria

- [ ] New file created: `docs/pages/ws-and-api-design/openapi-swagger.md`
- [ ] Content covers OpenAPI 3.0 specification
- [ ] Includes Swagger UI and Swagger Editor examples
- [ ] YAML and JSON schema examples included
- [ ] Linked from all pages that reference it
- [ ] Added to Web API Developer learning path

## Deliverables

### File: `openapi-swagger.md`

**Content Structure:**

```markdown
# OpenAPI and Swagger

![Beginner](https://img.shields.io/badge/Level-Beginner-green)
![Est. Time: 12min](https://img.shields.io/badge/Time-12min-green)

---

## Table of Contents
<!-- TOC -->
* [OpenAPI and Swagger](#openapi-and-swagger)
  * [Table of Contents](#table-of-contents)
  * [What is OpenAPI?](#what-is-openapi)
  * [What is Swagger?](#what-is-swagger)
  * [OpenAPI Specification](#openapi-specification)
  * [Writing OpenAPI Definitions](#writing-openapi-definitions)
  * [Swagger Tools](#swagger-tools)
  * [Best Practices](#best-practices)
  * [Example: Complete API Definition](#example-complete-api-definition)
  * [Ref.](#ref)
<!-- TOC -->

---

## What is OpenAPI?

[Definition of OpenAPI Specification (formerly Swagger Spec)]
[Current version: OpenAPI 3.0/3.1]
[Industry adoption and benefits]

## What is Swagger?

[Swagger as the tooling ecosystem]
[Relationship between OpenAPI and Swagger]
[Key Swagger tools overview]

## OpenAPI Specification

### Basic Structure

[YAML/JSON structure explanation]

```yaml
openapi: 3.0.0
info:
  title: Sample API
  version: 1.0.0
  description: Example API for documentation
servers:
  - url: https://api.example.com/v1
paths:
  /users:
    get:
      summary: List all users
      responses:
        '200':
          description: Success
```

### Components

#### Info Object
[Title, version, description, contact, license]

#### Servers Object
[API base URLs, variables]

#### Paths Object
[Endpoints and operations]

#### Components Object
[Reusable schemas, responses, parameters]

#### Security Schemes
[API key, OAuth2, Bearer token]

## Writing OpenAPI Definitions

### Defining Endpoints

[HTTP methods, parameters, request bodies, responses]

**Example:**
```yaml
paths:
  /users/{userId}:
    get:
      summary: Get user by ID
      parameters:
        - name: userId
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: User found
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          description: User not found
```

### Defining Data Models

[Using schemas and $ref]

**Example:**
```yaml
components:
  schemas:
    User:
      type: object
      required:
        - id
        - username
      properties:
        id:
          type: integer
          format: int64
        username:
          type: string
          minLength: 3
          maxLength: 50
        email:
          type: string
          format: email
        createdAt:
          type: string
          format: date-time
```

### Request Bodies

[POST/PUT request body examples]

### Authentication

[Security schemes: API Key, OAuth2, Bearer]

```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security:
  - bearerAuth: []
```

## Swagger Tools

### Swagger Editor

[Online editor for writing OpenAPI specs]
[Link: https://editor.swagger.io/]
[Features: syntax validation, real-time preview]

### Swagger UI

[Interactive API documentation]
[Try-it-out functionality]
[Embedding in web applications]

**Example Integration:**
```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="https://unpkg.com/swagger-ui-dist/swagger-ui.css">
</head>
<body>
  <div id="swagger-ui"></div>
  <script src="https://unpkg.com/swagger-ui-dist/swagger-ui-bundle.js"></script>
  <script>
    SwaggerUIBundle({
      url: 'https://api.example.com/openapi.yaml',
      dom_id: '#swagger-ui'
    });
  </script>
</body>
</html>
```

### Swagger Codegen

[Generating client SDKs and server stubs]
[Supported languages and frameworks]

### Alternative Tools

- Redoc (alternative documentation renderer)
- Postman (imports OpenAPI specs)
- Stoplight Studio (visual OpenAPI editor)

## Best Practices

### 1. Use Meaningful Descriptions

**❌ Poor:**
```yaml
summary: Get user
```

**✅ Good:**
```yaml
summary: Retrieve user details by ID
description: Returns a single user with complete profile information including email, creation date, and status.
```

### 2. Define Reusable Components

[Use $ref to avoid duplication]

### 3. Include Examples

```yaml
schema:
  $ref: '#/components/schemas/User'
example:
  id: 123
  username: johndoe
  email: john@example.com
```

### 4. Document Error Responses

[All possible error codes and meanings]

### 5. Version Your API

[URL versioning vs header versioning]

### 6. Use Tags for Organization

```yaml
tags:
  - name: Users
    description: User management operations
  - name: Orders
    description: Order processing
```

## Example: Complete API Definition

[Full working example of a simple REST API]

```yaml
openapi: 3.0.0
info:
  title: User Management API
  version: 1.0.0
  description: Simple API for user CRUD operations
  contact:
    name: API Support
    email: support@example.com

servers:
  - url: https://api.example.com/v1
    description: Production server
  - url: https://staging-api.example.com/v1
    description: Staging server

paths:
  /users:
    get:
      summary: List all users
      tags:
        - Users
      parameters:
        - name: limit
          in: query
          schema:
            type: integer
            default: 20
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/User'
    post:
      summary: Create new user
      tags:
        - Users
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserInput'
      responses:
        '201':
          description: User created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'

components:
  schemas:
    User:
      type: object
      properties:
        id:
          type: integer
        username:
          type: string
        email:
          type: string
          format: email
    UserInput:
      type: object
      required:
        - username
        - email
      properties:
        username:
          type: string
        email:
          type: string
          format: email

  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer

security:
  - bearerAuth: []
```

<sub>[Back to top](#table-of-contents)</sub>

---

## Ref.

**Official Resources:**
- [OpenAPI Specification](https://swagger.io/specification/)
- [OpenAPI 3.0 Guide](https://swagger.io/docs/specification/about/)
- [Swagger Tools](https://swagger.io/tools/)

**Tutorials:**
- [OpenAPI 3.0 Tutorial](https://support.smartbear.com/swaggerhub/docs/tutorials/openapi-3-tutorial.html)
- [Swagger Editor Guide](https://swagger.io/docs/open-source-tools/swagger-editor/)

**Tools:**
- [Swagger Editor](https://editor.swagger.io/)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)
- [Redoc](https://redocly.com/)
- [Stoplight Studio](https://stoplight.io/studio/)

---

[Get Started](../../get-started.md) | [RESTful API Design](restful/restful-api-design.md) | [Web Services & API Design](get-started.md#web-services-and-api-design)

---
```

## Technical Requirements

### Content Guidelines
- Breadth over depth - overview with links to official docs
- Include both YAML and JSON examples
- Show complete, working examples
- Focus on OpenAPI 3.0 (mention 3.1 differences if relevant)

### Visual Elements
- Consider Mermaid diagram showing OpenAPI ecosystem
- Code syntax highlighting (```yaml and ```json)
- Use comparison tables for version differences

### Cross-References
Update these files to link to new page:
- `docs/pages/ws-and-api-design/restful/restful-api-design.md` (6 references)
- `docs/pages/ws-and-api-design/restful/api-design-principles.md` (3 references)
- `docs/get-started.md` (add to Web Services section)

### Front Matter
```yaml
---
title: "OpenAPI and Swagger"
tags: [api, openapi, swagger, rest, documentation]
category: ws-and-api-design
difficulty: beginner
prerequisites:
  - restful-api-design
estimated_reading_time: 12
---
```

## Acceptance Criteria

**Content:**
- [ ] Explains difference between OpenAPI and Swagger
- [ ] Covers OpenAPI 3.0 specification structure
- [ ] Includes complete working example
- [ ] Documents all major Swagger tools
- [ ] Best practices section included

**Integration:**
- [ ] All 9 TODO references resolved
- [ ] Added to Web API Developer learning path
- [ ] Linked from relevant pages
- [ ] Navigation footer correct

**Quality:**
- [ ] YAML/JSON examples are valid
- [ ] Code blocks have language tags
- [ ] External links verified
- [ ] Follows template structure

## Testing Checklist

- [ ] Validate YAML examples with Swagger Editor
- [ ] All external links work
- [ ] No broken internal links
- [ ] Preview on GitHub renders correctly

## Dependencies

**Prerequisites:**
- Understanding of RESTful API concepts

**Related Tickets:**
- P1-T06 (Related Topics sections - can link to this)
- P2-T04 (Knowledge checks - can add quiz here)

## Resources

**Example OpenAPI Files:**
- [Petstore Example](https://github.com/swagger-api/swagger-petstore)
- [GitHub API](https://github.com/github/rest-api-description)
- [Stripe API](https://github.com/stripe/openapi)

**Tools for Testing:**
- [Swagger Editor](https://editor.swagger.io/) - validate examples
- [Swagger Validator](https://validator.swagger.io/) - validate URLs

## Notes

- Keep it practical - focus on common use cases
- This resolves 9 TODO references - high impact for effort
- Consider adding embedded Swagger UI demo (iframe)

## Assignee

TBD

## Due Date

End of Week 1 (Phase 1)
