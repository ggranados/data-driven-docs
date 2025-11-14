{% include mermaid.html %}
# Mermaid Test Page

This page tests Mermaid.js rendering.

## Test 1: Simple Flowchart

```mermaid
graph TD
    A[Start] --> B[Process]
    B --> C{Decision}
    C -->|Yes| D[Option 1]
    C -->|No| E[Option 2]
    D --> F[End]
    E --> F
```

## Test 2: Sequence Diagram

```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob!
    Bob->>Alice: Hello Alice!
    Alice->>Bob: How are you?
    Bob->>Alice: I'm good, thanks!
```

## Test 3: Class Diagram

```mermaid
classDiagram
    class Animal {
        +String name
        +int age
        +makeSound()
    }
    class Dog {
        +bark()
    }
    class Cat {
        +meow()
    }
    Animal <|-- Dog
    Animal <|-- Cat
```

## Test 4: With Green Theme

```mermaid
graph LR
    A[Client] -->|Request| B[Server]
    B -->|Response| A
    style A fill:#00ff00,stroke:#00ff00,color:#000
    style B fill:#00ff00,stroke:#00ff00,color:#000
```

---

If you see diagrams above, Mermaid is working! If not, check browser console for errors.

[Back to Home](index.md)
