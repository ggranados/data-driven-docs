# Diagram Conversion Example: Mermaid → PlantUML

This document shows how to convert the Thread Memory Architecture diagram from Mermaid to PlantUML.

## Original Mermaid Diagram (Not Working)

**File:** `docs/pages/programming/languages/java/java-8/concurrency/java-memory-model.md`

````markdown
```mermaid
graph TD
    subgraph "Thread 1"
        T1Stack[Stack<br/>Local Variables]
        T1Cache[CPU Cache<br/>Thread 1]
    end

    subgraph "Thread 2"
        T2Stack[Stack<br/>Local Variables]
        T2Cache[CPU Cache<br/>Thread 2]
    end

    subgraph "Main Memory"
        Heap[Heap<br/>Shared Objects]
        Static[Static Variables<br/>Class Data]
    end

    T1Stack -->|reads/writes| T1Cache
    T2Stack -->|reads/writes| T2Cache
    T1Cache <-->|eventual sync| Heap
    T2Cache <-->|eventual sync| Heap

    style Heap fill:#ffe1e1
    style Static fill:#ffe1e1
    style T1Cache fill:#e1f5ff
    style T2Cache fill:#e1f5ff
    style T1Stack fill:#fff4e1
    style T2Stack fill:#fff4e1
```
````

## Converted PlantUML Version (Working)

### PlantUML Source Code

```plantuml
@startuml
skinparam backgroundColor #0d1117
skinparam componentBackgroundColor #1a1a1a
skinparam componentBorderColor #00ff00
skinparam arrowColor #00ff00

package "Thread 1" #fff4e1 {
  [Stack\nLocal Variables] as T1Stack
  [CPU Cache\nThread 1] as T1Cache
}

package "Thread 2" #fff4e1 {
  [Stack\nLocal Variables] as T2Stack
  [CPU Cache\nThread 2] as T2Cache
}

package "Main Memory" #ffe1e1 {
  [Heap\nShared Objects] as Heap
  [Static Variables\nClass Data] as Static
}

T1Stack --> T1Cache : reads/writes
T2Stack --> T2Cache : reads/writes
T1Cache <--> Heap : eventual\nsync
T2Cache <--> Heap : eventual\nsync
@enduml
```

### How to Generate the Image

**Option 1: Use PlantUML Web Server**

1. Go to: http://www.plantuml.com/plantuml/uml/
2. Paste the PlantUML code above
3. Click "Submit"
4. Copy the generated URL

**Option 2: Use PlantUML Command Line**

```bash
plantuml diagram.puml -tsvg
```

### Markdown Usage

Replace the Mermaid code block with:

```markdown
<!-- PlantUML Source:
@startuml
skinparam backgroundColor #0d1117
skinparam componentBackgroundColor #1a1a1a
skinparam componentBorderColor #00ff00
skinparam arrowColor #00ff00

package "Thread 1" #fff4e1 {
  [Stack\nLocal Variables] as T1Stack
  [CPU Cache\nThread 1] as T1Cache
}

package "Thread 2" #fff4e1 {
  [Stack\nLocal Variables] as T2Stack
  [CPU Cache\nThread 2] as T2Cache
}

package "Main Memory" #ffe1e1 {
  [Heap\nShared Objects] as Heap
  [Static Variables\nClass Data] as Static
}

T1Stack --> T1Cache : reads/writes
T2Stack --> T2Cache : reads/writes
T1Cache <--> Heap : eventual\nsync
T2Cache <--> Heap : eventual\nsync
@enduml
-->

![Thread Memory Architecture](http://www.plantuml.com/plantuml/svg/TP71ReCm48Nl-HN3dqgmA8KQeIf4RIGe2Lqx9wOaDqxQN2tlt-t2YQPsLIJtt_kzl-EVZ7wCKXvLKAd4OYpTUB51Y89Mq3L9GhQYXk36uVE_mhZVwwdKFkGPqWOGbJxKmcIXaBRpvZpKVQZOPW5dPDHlEwwkKlOQBkW7aPPW6WnOjNWwOD5Kz3Z5gZxI_M5qn_Hzhvzm4Vz3Vp-sF_JNq-_bST-wYjvzZZpF-Vp_k-V_WzxFl_0)
```

## Other Diagram Conversions Needed

### 1. Synchronized Block Sequence (java-memory-model.md)

**Mermaid:**
```mermaid
sequenceDiagram
    participant T1 as Thread 1
    participant Lock
    participant Memory as Main Memory
    participant T2 as Thread 2
    ...
```

**PlantUML:**
```plantuml
@startuml
participant "Thread 1" as T1
participant Lock
participant "Main Memory" as Memory
participant "Thread 2" as T2

T1 -> Lock: acquire lock
T1 -> T1: counter = 1
T1 -> Memory: flush all changes\nto main memory
T1 -> Lock: release lock
note over Memory: counter = 1 visible

T2 -> Lock: acquire lock
T2 -> Memory: read latest values\nfrom main memory
T2 -> T2: sees counter = 1
T2 -> Lock: release lock
@enduml
```

### 2. Optimistic Reading Flow (locks-and-conditions.md)

**Mermaid:**
```mermaid
graph TD
    A[Start Optimistic Read] --> B[Get stamp]
    ...
```

**PlantUML:**
```plantuml
@startuml
start
:Start Optimistic Read;
:Get stamp;
:Read data;
if (Validate stamp?) then (Valid)
  :Return data - No lock needed!;
else (Invalid)
  :Acquire read lock;
  :Re-read data;
  :Release lock;
  :Return data;
endif
stop
@enduml
```

### 3. Divide-and-Conquer (fork-join.md)

**Mermaid:**
```mermaid
graph TD
    A[Large Task] --> B[Fork]
    ...
```

**PlantUML:**
```plantuml
@startuml
start
:Large Task;
fork
  :Subtask 1;
  :Process;
fork again
  :Subtask 2;
  fork
    :Subtask 2.1;
    :Process;
  fork again
    :Subtask 2.2;
    :Process;
  end fork
end fork
:Join;
:Final Result;
stop
@enduml
```

### 4. Future Execution Flow (callable-and-future.md)

**Mermaid:**
```mermaid
sequenceDiagram
    participant Client
    participant Executor
    participant WorkerThread
    participant Future
    ...
```

**PlantUML:**
```plantuml
@startuml
participant Client
participant Executor
participant WorkerThread
participant Future

Client -> Executor: submit(Callable)
Executor -> Future: create Future<T>
Executor --> Client: return Future
note over Client: Can do other work

Executor -> WorkerThread: assign task
WorkerThread -> WorkerThread: execute callable.call()

alt Task completes successfully
    WorkerThread -> Future: set result(value)
    Client -> Future: get()
    Future --> Client: return value
else Task throws exception
    WorkerThread -> Future: set exception(e)
    Client -> Future: get()
    Future --> Client: throw ExecutionException
else Task is cancelled
    Client -> Future: cancel(true)
    Future -> WorkerThread: interrupt()
    WorkerThread -> Future: set cancelled
    Client -> Future: get()
    Future --> Client: throw CancellationException
end
@enduml
```

## Summary

**Files to Update:**
1. `java-8/concurrency/java-memory-model.md` - 2 diagrams
2. `java-8/concurrency/locks-and-conditions.md` - 1 diagram
3. `java-8/concurrency/fork-join.md` - 1 diagram
4. `java-8/concurrency/callable-and-future.md` - 1 diagram

**Total:** 5 Mermaid diagrams to convert to PlantUML

**Benefits After Conversion:**
- ✅ Diagrams will render on GitHub Pages
- ✅ No JavaScript required
- ✅ Works in all browsers
- ✅ Can be updated easily via PlantUML web editor
- ✅ Source code preserved in HTML comments

---

See [PLANTUML-SETUP.md](PLANTUML-SETUP.md) for complete PlantUML documentation.
