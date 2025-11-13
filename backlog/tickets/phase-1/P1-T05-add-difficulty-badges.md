# P1-T05: Add Difficulty Badges to All Pages

**Phase:** 1 - Foundation
**Week:** 2 - Navigation & Structure
**Priority:** Medium
**Effort:** 10 hours
**Status:** Not Started

---

## Objective

Add difficulty level badges, technology version badges, and reading time estimates to all 60+ documentation pages for improved user expectations and navigation.

## Context

Currently, users can't tell at a glance:
- How difficult a topic is (prerequisite knowledge needed)
- Which technology version is required
- How long it will take to read

Adding visual badges improves:
- User expectations
- Learning path planning
- Professional appearance
- Content discovery

## Success Criteria

- [ ] All 60+ pages have difficulty badges
- [ ] Version-specific content has technology badges
- [ ] Reading time estimates added to longer pages (>10 min)
- [ ] Template.md updated with badge standards
- [ ] Consistent badge styling across all pages

## Deliverables

### Badge Types to Add

#### 1. Difficulty Level Badges
**Format:** `![{Level}](https://img.shields.io/badge/Level-{Level}-{color})`

**Levels:**
- 🟢 **Beginner** (green) - No prerequisites, fundamental concepts
- 🟡 **Intermediate** (yellow) - Requires basic knowledge
- 🔴 **Advanced** (red) - Complex topics, multiple prerequisites

**Examples:**
```markdown
![Beginner](https://img.shields.io/badge/Level-Beginner-green)
![Intermediate](https://img.shields.io/badge/Level-Intermediate-yellow)
![Advanced](https://img.shields.io/badge/Level-Advanced-red)
```

#### 2. Technology Version Badges
**Format:** `![{Tech} {Version}+](https://img.shields.io/badge/{Tech}-{Version}+-blue)`

**Examples:**
```markdown
![Java 8+](https://img.shields.io/badge/Java-8+-blue)
![Java 21+](https://img.shields.io/badge/Java-21+-blue)
![Spring Boot 3](https://img.shields.io/badge/Spring%20Boot-3-green)
```

#### 3. Status Badges (for preview/experimental features)
```markdown
![Stable](https://img.shields.io/badge/Status-Stable-green)
![Preview](https://img.shields.io/badge/Status-Preview-yellow)
![Experimental](https://img.shields.io/badge/Status-Experimental-orange)
![LTS](https://img.shields.io/badge/LTS-8%2C%2011%2C%2017%2C%2021-green)
```

#### 4. Reading Time Estimates
**Format:** `![Est. Time: Xmin](https://img.shields.io/badge/Time-Xmin-green)`

**Calculation:**
- Word count ÷ 200 words/min
- +1 minute per code example
- Round to nearest 5 minutes

**Examples:**
```markdown
![Est. Time: 10min](https://img.shields.io/badge/Time-10min-green)
![Est. Time: 15min](https://img.shields.io/badge/Time-15min-green)
![Est. Time: 20min](https://img.shields.io/badge/Time-20min-orange)
```

### Placement in Documents

**Standard placement:**
```markdown
# Page Title

![Difficulty Badge] ![Tech Version Badge] ![Reading Time Badge]

---

## Table of Contents
[TOC]

---

[Content begins...]
```

**Example (Stream API):**
```markdown
# Streams

![Intermediate](https://img.shields.io/badge/Level-Intermediate-yellow)
![Java 8+](https://img.shields.io/badge/Java-8+-blue)
![Est. Time: 15min](https://img.shields.io/badge/Time-15min-green)

---

## Table of Contents
<!-- TOC -->
...
```

## Page-by-Page Badge Assignment

### Programming / Java

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| java.md | Beginner | Java 8+ | 10min |
| develop.md | Beginner | Java 8+ | 8min |
| lambda-expression.md | Beginner | Java 8+ | 12min |
| stream-api.md | Intermediate | Java 8+ | 15min |
| optional.md | Intermediate | Java 8+ | 10min |
| project-reactor.md | Advanced | Java 8+ | 30min |
| generics.md | Intermediate | Java 5+ | 15min |
| enhanced-collections.md | Intermediate | Java 5+ | 18min |
| fp.md | Intermediate | Java 8+ | 15min |
| concurrency.md | Advanced | Java 8+ | 12min |
| executors.md | Advanced | Java 8+ | 15min |
| callable-and-future.md | Advanced | Java 8+ | 12min |
| completable-future.md | Advanced | Java 8+ | 15min |
| java-memory-model.md | Advanced | Java 8+ | 15min |

### Programming / Paradigms

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| object-oriented.md | Beginner | - | 12min |
| functional.md | Intermediate | - | 15min |
| reactive.md | Intermediate | - | 12min |
| declarative.md | Beginner | - | 8min |
| imperative.md | Beginner | - | 8min |
| procedural.md | Beginner | - | 8min |
| structured.md | Beginner | - | 8min |

### Database Management

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| acid.md | Beginner | - | 8min |
| base.md | Intermediate | - | 8min |
| cap.md | Intermediate | - | 10min |
| relational.md | Beginner | - | 10min |
| nosql.md | Intermediate | - | 10min |

### Web Services & API Design

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| restful.md | Beginner | - | 12min |
| restful-api-design.md | Intermediate | - | 20min |
| api-design-principles.md | Intermediate | - | 15min |
| resource-design-representation.md | Intermediate | - | 12min |
| oauth.md | Intermediate | OAuth 2.0 | 15min |
| jwt.md | Beginner | - | 10min |
| saml.md | Intermediate | - | 12min |
| openid-connect.md | Intermediate | OIDC 1.0 | 12min |
| authn-authz.md | Beginner | - | 10min |
| openapi-swagger.md | Beginner | OpenAPI 3.0 | 12min |

### Design Patterns

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| solid.md | Intermediate | - | 15min |
| observer.md | Intermediate | - | 12min |

### Architectural Patterns

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| microservices.md | Advanced | - | 18min |
| reactive.md | Advanced | - | 15min |

### Cyber-security

| File | Difficulty | Version | Time |
|------|------------|---------|------|
| iam.md | Beginner | - | 10min |
| sql-injection.md | Intermediate | - | 15min |
| xss-prevention.md | Intermediate | - | 15min |
| owasp-top-10.md | Beginner | - | 12min |

## Technical Requirements

### Badge Services
- Use shields.io for consistent styling
- Format: `https://img.shields.io/badge/{label}-{message}-{color}`
- Colors: green, yellow, orange, red, blue

### Automation Script (Optional)
Create script to add badges based on CSV file:

```java
// BadgeAdder.java
public class BadgeAdder {
    public static void main(String[] args) {
        // Read CSV with file paths and badge info
        // Update each markdown file with badges
        // Preserve existing content
    }
}
```

### Update Template
`docs/pages/common/template.md`:
```markdown
# H1

![Difficulty Badge Here]
![Tech Version Badge If Applicable]
![Reading Time Badge]

---

## Table of Contents
[TOC]
```

## Acceptance Criteria

**Completeness:**
- [ ] All 60+ pages have difficulty badges
- [ ] Version-specific pages have technology badges
- [ ] Pages >10min reading have time estimates
- [ ] Template.md updated

**Consistency:**
- [ ] Same badge format across all pages
- [ ] Correct difficulty levels applied
- [ ] Technology versions accurate
- [ ] Reading times reasonable

**Quality:**
- [ ] Badges render correctly on GitHub
- [ ] Mobile-friendly display
- [ ] Colors are accessible (contrast)
- [ ] No broken badge URLs

## Testing Checklist

- [ ] Preview 10+ random pages on GitHub
- [ ] Test on mobile device
- [ ] Verify badges load quickly
- [ ] Check color accessibility
- [ ] Validate all shield.io URLs

## Dependencies

**Prerequisites:**
- None (can start immediately)

**Related Tickets:**
- P1-T04 (Learning paths - badges help path navigation)
- P1-T06 (Related topics - can reference difficulty levels)
- P2-T06 (Reading times - this ticket adds foundation)

## Resources

**Badge Service:**
- [Shields.io](https://shields.io/) - Badge generation
- [Badge Format Guide](https://shields.io/category/size)

**Examples:**
- [Awesome README](https://github.com/matiassingers/awesome-readme) - Badge examples
- [Markdown Badges](https://github.com/Ileriayo/markdown-badges)

## Implementation Steps

1. **Create badge mapping** (2 hours)
   - Review all 60+ pages
   - Assign difficulty levels
   - Estimate reading times
   - Create CSV/spreadsheet

2. **Update template** (30 min)
   - Add badges to template.md
   - Document badge standards

3. **Add badges to pages** (6 hours)
   - Manually add to each file
   - OR create automation script
   - Follow consistent format

4. **Validation** (1 hour)
   - Preview sample pages
   - Test on mobile
   - Fix any issues

5. **Documentation** (30 min)
   - Update CLAUDE.md with badge standards
   - Add note to contribution guide

## Notes

- This is somewhat tedious but high-value work
- Consider automation to speed up process
- Difficulty levels are subjective - use best judgment
- Can iterate based on user feedback
- Front matter metadata can later be used to auto-generate badges

## Future Enhancements

- Auto-generate badges from front matter
- Add "Prerequisites" badges (e.g., "Requires: Lambda Expressions")
- Add "Updated" date badges
- Visual difficulty curve in learning paths

## Assignee

TBD

## Due Date

End of Week 2 (Phase 1)
