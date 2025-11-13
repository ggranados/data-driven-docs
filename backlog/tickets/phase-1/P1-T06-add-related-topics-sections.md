# P1-T06: Add "Related Topics" Sections to Priority Pages

**Phase:** 1 - Foundation
**Week:** 2 - Navigation & Structure
**Priority:** High
**Effort:** 15 hours
**Status:** Not Started

---

## Objective

Add structured "Related Topics" sections to 25 priority pages to improve content discoverability, establish logical learning progressions, and reduce orphaned content.

## Context

Currently, pages have minimal cross-referencing:
- Users don't know what to learn next
- Related concepts are disconnected
- Learning progression is unclear
- Decreases time on site and engagement

"Related Topics" sections will:
- Guide natural learning progression
- Show prerequisite relationships
- Suggest next steps
- Improve SEO through internal linking
- Reduce bounce rate

## Success Criteria

- [ ] 25 high-traffic pages have "Related Topics" sections
- [ ] Each section includes 3-5 categories (Prerequisites, Next Steps, Related Patterns, etc.)
- [ ] All linked topics exist or marked as planned
- [ ] Consistent format across all pages
- [ ] Template.md updated with standard structure

## Deliverables

### Standard "Related Topics" Section Format

**Placement:** After main content, before References section

**Structure:**
```markdown
---

## Related Topics

### Prerequisites
- [Topic Name](path/to/topic.md) - Brief description
- [Topic Name](path/to/topic.md) - Brief description

### Next Steps
- [Topic Name](path/to/topic.md) - Brief description
- [Topic Name](path/to/topic.md) - Brief description

### Related Patterns/Concepts
- [Topic Name](path/to/topic.md) - Brief description
- [Topic Name](path/to/topic.md) - Brief description

### Deep Dives
- [Topic Name](path/to/topic.md) - Brief description
- [Topic Name](path/to/topic.md) ⏳ - Planned content

### Official Resources
- [External Link](https://example.com) - Resource description

---

## Ref.
[Existing references section]
```

### Priority Pages (25 pages)

#### High Traffic Pages (15 pages)
1. **stream-api.md** - Central Java 8 topic
2. **lambda-expression.md** - Fundamental Java 8 concept
3. **optional.md** - Common Java pattern
4. **project-reactor.md** - Advanced reactive topic
5. **restful-api-design.md** - Core API design
6. **oauth.md** - Popular security topic
7. **jwt.md** - Authentication standard
8. **microservices.md** - Architecture pattern
9. **solid.md** - Core design principles
10. **acid.md** - Database fundamental
11. **nosql.md** - Database category
12. **functional.md** - Programming paradigm
13. **reactive.md** - Architecture paradigm
14. **object-oriented.md** - Core paradigm
15. **enhanced-collections.md** - Java collections

#### Foundation Pages (10 pages)
16. **java.md** - Java overview
17. **concurrency.md** - Java threading
18. **completable-future.md** - Async programming
19. **generics.md** - Java type system
20. **api-design-principles.md** - API fundamentals
21. **resource-design-representation.md** - REST concepts
22. **openid-connect.md** - Identity protocol
23. **observer.md** - Design pattern
24. **cap.md** - Distributed systems
25. **base.md** - NoSQL principle

### Example Implementation: stream-api.md

```markdown
---

## Related Topics

### Prerequisites
Recommended topics to understand before diving into Streams:

- [Java Collections Framework](../java-5/enhanced-collections.md) - Understanding of List, Set, Map interfaces and their implementations
- [Lambda Expressions](lambda-expression.md) - Anonymous functions used extensively in stream operations
- [Functional Interfaces](lambda-expression.md#functional-interfaces) - Single abstract method interfaces that enable lambda usage
- [Generics](../java-5/generics.md) - Type parameters used throughout the Stream API

### Next Steps
After mastering Streams, explore these related topics:

- [Optional API](optional.md) - Handling null values in functional style, often used with stream results
- [Parallel Streams](stream-api.md#parallel-streams) - Performance optimization with parallel processing
- [Collectors](stream-api.md#collectors) - Advanced result gathering techniques
- [Method References](lambda-expression.md#method-references) - Shorthand for lambda expressions in streams

### Related Patterns
Streams connect to these broader concepts:

- [Functional Programming Paradigm](../../paradigms/functional.md) - Declarative approach to data processing
- [Iterator Pattern](../../design-patterns/behavioral/) ⏳ - Alternative approach to collection traversal
- [Observer Pattern](../../design-patterns/behavioral/observer.md) - Event-driven data processing pattern

### Deep Dives
Advanced topics building on Streams:

- [Project Reactor](project-reactor.md) - Reactive streams for asynchronous, non-blocking processing
- [CompletableFuture](concurrency/completable-future.md) - Asynchronous computation with stream-like chaining
- [RxJava]() ⏳ - Alternative reactive programming library for Java

### Performance & Best Practices
- [Java Memory Model](concurrency/java-memory-model.md) - Understanding thread-safety in parallel streams
- [Stream Performance Guide]() ⏳ - When to use sequential vs parallel streams

### Official Resources
- [Java Stream API Javadoc](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html)
- [Java Tutorials: Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/)
- [Java 8 Stream API Guide](https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html)

---

## Ref.
[Existing references...]
```

### Example Implementation: oauth.md

```markdown
---

## Related Topics

### Prerequisites
Foundation knowledge for understanding OAuth:

- [Authentication vs Authorization](authn-authz.md) - Core security concepts and differences
- [HTTP Basics]() ⏳ - Understanding of HTTP methods, status codes, headers
- [RESTful APIs](../restful.md) - OAuth operates over HTTP REST endpoints

### Next Steps
Building on OAuth knowledge:

- [JWT (JSON Web Tokens)](jwt.md) - Token format commonly used with OAuth 2.0
- [OpenID Connect](openid-connect.md) - Identity layer built on top of OAuth 2.0
- [API Security Best Practices]() ⏳ - Securing APIs with OAuth

### Related Protocols
Alternative or complementary authentication methods:

- [SAML](saml.md) - XML-based authentication protocol for enterprise SSO
- [OpenID Connect](openid-connect.md) - OAuth 2.0 extension for authentication
- [Kerberos]() ⏳ - Network authentication protocol

### Implementation Guides
Framework-specific OAuth implementations:

- [Spring Security OAuth]() ⏳ - OAuth in Spring Boot applications
- [OAuth in Single Page Apps]() ⏳ - SPA authentication patterns

### Security Considerations
- [IAM (Identity and Access Management)](../../cyber-security/access-control-and-authn/iam.md) - Broader identity management context
- [OWASP Top 10](../../cyber-security/owasp-top-10.md) - Web application security risks
- [Token Storage Best Practices]() ⏳ - Securely storing access tokens

### Official Resources
- [OAuth 2.0 RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749)
- [OAuth 2.0 Playground](https://www.oauth.com/playground/)
- [Auth0 OAuth Documentation](https://auth0.com/docs/protocols/oauth2)

---

## Ref.
[Existing references...]
```

## Technical Requirements

### Content Guidelines
- **Prerequisites**: Topics users should know first (1-4 items)
- **Next Steps**: Natural progression after this topic (2-4 items)
- **Related Patterns/Concepts**: Parallel or complementary topics (2-4 items)
- **Deep Dives**: Advanced extensions of current topic (1-3 items)
- **Official Resources**: External authoritative sources (2-4 items)

### Link Format
```markdown
- [Topic Title](relative/path.md) - Brief one-sentence description
- [Planned Topic]() ⏳ - Description of what will be covered
```

### Descriptions
- One sentence per link (10-15 words)
- Explain **why** the link is relevant
- Use action words (understanding, exploring, implementing)

### Categories to Use
Choose 3-5 categories based on page context:
- Prerequisites (foundational topics)
- Next Steps (natural progression)
- Related Patterns/Concepts (parallel topics)
- Related Protocols (for security/API topics)
- Deep Dives (advanced extensions)
- Implementation Guides (framework-specific)
- Performance & Best Practices (optimization)
- Security Considerations (for web topics)
- Official Resources (external links)

## Acceptance Criteria

**Completeness:**
- [ ] All 25 priority pages have Related Topics sections
- [ ] Each page has 3-5 appropriate categories
- [ ] Each category has 1-4 links
- [ ] Total of 8-15 related items per page

**Quality:**
- [ ] All internal links verified (exist or marked ⏳)
- [ ] Descriptions are clear and helpful
- [ ] Categories are logically chosen
- [ ] No circular references (A→B→A)
- [ ] Bidirectional linking where appropriate

**Consistency:**
- [ ] Same format across all pages
- [ ] Consistent category names
- [ ] Same markdown style
- [ ] Placement before Ref. section

**Integration:**
- [ ] Template.md updated
- [ ] CLAUDE.md documents standard
- [ ] Contribution guide references standard

## Testing Checklist

- [ ] All internal links work
- [ ] External links valid
- [ ] No broken references
- [ ] Preview 5+ pages on GitHub
- [ ] Mobile rendering acceptable
- [ ] Links open in correct location

## Dependencies

**Requires:**
- P1-T01 (Java concurrency) - Complete before adding related topics to those pages
- P1-T02 (OpenAPI) - Complete before adding related topics to API pages
- P1-T03 (Security) - Complete before adding related topics to security pages

**Enhances:**
- P1-T04 (Learning paths) - Related topics support learning progressions
- P1-T05 (Badges) - Difficulty info helps choose related topics

## Resources

**Link Analysis:**
- Review existing internal links in pages
- Use MarkdownFileReferences.java to find connection patterns
- Identify most-referenced topics

**Content Mapping:**
```
stream-api.md
├── Prerequisites: Collections, Lambdas, Generics
├── Next: Optional, Collectors, Parallel Streams
├── Related: Functional Programming, Iterator Pattern
└── Deep Dive: Project Reactor, RxJava

oauth.md
├── Prerequisites: AuthN/AuthZ, HTTP, REST
├── Next: JWT, OpenID Connect, API Security
├── Related: SAML, Kerberos
└── Implementation: Spring Security, SPA patterns
```

## Implementation Steps

1. **Create relationship map** (2 hours)
   - For each of 25 pages, list:
     - What knowledge is required (prerequisites)
     - What comes next (progression)
     - What's parallel (related)
     - What's advanced (deep dive)

2. **Draft related topics sections** (8 hours)
   - Write sections for all 25 pages
   - Follow standard format
   - Verify all links

3. **Add to markdown files** (3 hours)
   - Edit each file
   - Place before Ref. section
   - Maintain existing formatting

4. **Update template and docs** (1 hour)
   - Update template.md
   - Update CLAUDE.md
   - Update contribution guide

5. **Validation** (1 hour)
   - Run MarkdownFileReferences.java
   - Fix any broken links
   - Preview sample pages

## Notes

- Start with most popular pages (stream-api, oauth, microservices)
- This significantly improves navigation and SEO
- Creates "web" of interconnected content
- Future: could auto-generate relationship graphs from this data
- Be mindful of creating too many ⏳ planned items

## Future Enhancements

- Auto-generate relationship graph visualization
- Add "Reading order" indicators (1/5, 2/5, etc.)
- Difficulty-based filtering ("Show beginner topics only")
- Track most common learning paths from analytics

## Assignee

TBD

## Due Date

End of Week 2 (Phase 1)
