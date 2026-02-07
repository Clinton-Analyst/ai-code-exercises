# Code Understanding Journal - Python Task Manager

**Student:** Clinton Munene 
**Date:** February 7, 2026

---

## FILES I FOUND

### 1. README
**My guess about what it does:** 
This is where documentation is done 


### 2. cli.py
**My guess about what it does:** 
Honestly, no idea what this does 


### 3. models.py
**My guess about what it does:**  
This is where training of the features takes place


### 4. storage.py
**My guess about what it does:**  
task are stored in here after 


### 5. task_manager.py
**My guess about what it does:**  
This is the main app that we are creating


### 6. tests (folder)
**My guess about what it does:**  
where testing of codes is done

---

## OBSERVATIONS

### First Impressions:
I easily identified files 

### Questions I Have:
kindly validate my thinking and also correct where i might go wrong

## CLARIFICATIONS FROM AI
### 1. README
**My guess about what it does:** 
README files explain what the project does, how to set it up, and how to use it.


### 2. cli.py
**My guess about what it does:** 
CLI = Command Line Interface. This file probably handles how users interact with the task manager through the terminal (typing commands, showing menus, getting input).


### 3. models.py
**My guess about what it does:**  
the blueprint/structure of what a "Task" looks like (e.g., a task has a title, description, due date, etc.). Think of it as defining the shape of your data, not machine learning.


### 4. storage.py
**My guess about what it does:**  
 This likely handles saving tasks to a file or database and loading them back.

### 5. task_manager.py
**My guess about what it does:**  
This is probably the "brain" - the core logic that manages tasks (add, delete, update, list tasks).


### 6. tests (folder)
**My guess about what it does:**  
Contains automated tests to make sure the code works correctly.


---

## DEEP DIVE: TASK CREATION & MANAGEMENT (models.py)

### 1. Main Components Involved in Task Creation/Updates

**Three Key Components Work Together:**

**a) Enumerations (Enums):**
- `TaskPriority`: Defines priority levels (LOW, MEDIUM, HIGH, URGENT)
- `TaskStatus`: Defines task states (TODO, IN_PROGRESS, REVIEW, DONE)
- **Purpose:** Prevent invalid values and make code more readable

**b) Task Class (`__init__` method):**
- Creates new task objects with all necessary properties
- Auto-generates unique ID using uuid
- Sets default values (status = TODO, timestamps, etc.)
- **Properties created:** id, title, description, priority, status, created_at, updated_at, due_date, completed_at, tags

**c) Task Methods (behaviors):**
- `update(**kwargs)`: Modifies any task property dynamically
- `mark_as_done()`: Changes status to DONE and records completion time
- `is_overdue()`: Checks if task is past due date and not completed

### 2. Execution Flow

**When a Task is Created:**
```
Step 1: Another file calls Task("Title", "Description", TaskPriority.HIGH)
   ↓
Step 2: __init__ method executes automatically
   ↓
Step 3: Unique ID generated (uuid.uuid4())
   ↓
Step 4: All properties initialized:
   - User-provided: title, description, priority, due_date, tags
   - Auto-set: id, status (TODO), created_at, updated_at, completed_at (None)
   ↓
Step 5: Task object returned, ready to use
```

**When a Task is Updated:**
```
Step 1: task.update(title="New Title", priority=TaskPriority.URGENT)
   ↓
Step 2: update() method loops through each argument
   ↓
Step 3: For each property:
   - Check if it exists on the task (hasattr)
   - If yes, update it (setattr)
   - If no, skip it (prevents errors)
   ↓
Step 4: updated_at timestamp refreshed to now
   ↓
Step 5: Changes complete
```

**When a Task is Marked as Done:**
```
Step 1: task.mark_as_done()
   ↓
Step 2: Status changed to TaskStatus.DONE
   ↓
Step 3: completed_at set to current time
   ↓
Step 4: updated_at also set to current time
```

### 3. How Data is Stored and Retrieved

**Storage Strategy (based on models.py analysis):**

- **models.py DOES NOT handle storage** - it only defines the structure
- Task objects exist in memory (RAM) while program runs
- Other files (likely storage.py) handle:
  - Converting Task objects to a format that can be saved (serialization)
  - Saving to file/database
  - Loading from file/database
  - Converting back to Task objects (deserialization)

**Data Flow:**
```
Task object (in memory)
   ↓ (when saving)
storage.py converts to JSON/dict
   ↓
Saved to file
   ↓ (when loading)
storage.py reads file
   ↓
Recreates Task object in memory
```

**Key Insight:** Separation of concerns - models.py focuses on WHAT a task is, not WHERE it's stored.

### 4. Interesting Design Patterns Discovered

**Pattern 1: Enumeration Pattern**
- **What:** Using Enums for fixed sets of values (Priority, Status)
- **Why it's smart:** 
  - Prevents typos (TaskStatus.DONE vs "done" vs "Done" vs "DONE")
  - Auto-completion in code editors
  - Can't set invalid values
  - Self-documenting code

**Pattern 2: Automatic Timestamp Management**
- **What:** created_at and updated_at automatically set/updated
- **Why it's smart:**
  - No manual tracking needed
  - Audit trail built-in
  - Can't forget to update timestamps

**Pattern 3: Single Responsibility Principle**
- **What:** Task class ONLY defines task structure and behavior
- **Why it's smart:**
  - Doesn't mix concerns (no storage, no display logic)
  - Easy to test
  - Can change storage method without touching Task class
  - Reusable in different contexts

**Pattern 4: Defensive Programming (`hasattr` in update())**
- **What:** Checks if property exists before updating
- **Why it's smart:**
  - Prevents crashes from typos: `task.update(titel="X")` won't break the app
  - Silent failure = more robust code
  - User mistakes don't crash the system

**Pattern 5: UUID for Unique Identifiers**
- **What:** Using uuid4() instead of sequential numbers
- **Why it's smart:**
  - Guaranteed uniqueness (even across different computers/databases)
  - No collision risks
  - Can generate IDs without checking database
  - Works in distributed systems

---

---

## CODE EXPLORATION: TASK PRIORITY FEATURE

**Date Started:** February 7, 2026  
**Status:** In Progress

---

### MY INITIAL UNDERSTANDING (Before Investigation)

**What I thought I knew:**
- Task creation involves asking for title, description, and priority value
- Task priority can be filtered from list_task
- Updates can be done on task priority
- Priority counts can be returned
- Main file involved: task_manager.py

**What was unclear to me:**
- How the execution actually gets triggered
- The complete flow from user input to task creation
- How the files work together in practice

---

### INVESTIGATION PROCESS

#### Question 1: Understanding create_task/add_task function

**File:** task_manager.py

**Function found:**
```
[Write the function name and signature here]
```

**Parameters it accepts:**
- 
- 
- 

**What it does:**
[Your description]

**What it returns:**
[Your findings]

**Does it use the Task class from models.py?**
[Yes/No and how]

---

#### Question 2: Priority-related functions

**Functions I found:**
1. Function name: ________________
   - Purpose: 
   - Parameters: 
   - Return value: 

2. Function name: ________________
   - Purpose: 
   - Parameters: 
   - Return value: 

---

#### Question 3: The CLI Entry Point

**File:** cli.py


---

#### Question 4: Data Flow Journey

**Tracing: "User creates a HIGH priority task"**
```
Step 1: User interaction
→ [What happens in cli.py?]

Step 2: Input gathering
→ [How are title, description, priority collected?]

Step 3: Task creation
→ [Which function in task_manager.py is called?]

Step 4: Task object creation
→ [Does it use models.py Task class?]

Step 5: Storage
→ [Where does the task go? Stored in memory? Saved to file?]

Step 6: Confirmation
→ [How does user know it succeeded?]
```

---

## DATA FLOW ANALYSIS: TASK COMPLETION

**Feature:** Marking a task as complete  
**Entry Point:** `TaskManager.update_task_status(task_id, "done")`

### Complete Data Flow Diagram

### 3. COMPLETE DATA FLOW DIAGRAM
```
┌─────────────────────────────────────────────────────────────┐
│                    USER INTERACTION                          │
│  User selects: "Mark task #abc123 as complete"              │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                     CLI.PY LAYER                             │
│  - Validates task_id exists                                  │
│  - Gets status choice from user (or "done" is hardcoded)    │
│  - Calls: task_manager.update_task_status(task_id, "done")  │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│              TASK_MANAGER.PY - BUSINESS LOGIC                │
│                                                              │
│  update_task_status(task_id, new_status_value):             │
│                                                              │
│  ┌────────────────────────────────────────────────────┐    │
│  │ Step 1: VALIDATION                                  │    │
│  │ new_status = TaskStatus(new_status_value)          │    │
│  │ (Converts "done" → TaskStatus.DONE enum)           │    │
│  │ (Raises ValueError if invalid)                     │    │
│  └────────────────────────────────────────────────────┘    │
│                         │                                    │
│                         ▼                                    │
│  ┌────────────────────────────────────────────────────┐    │
│  │ Step 2: SPECIAL DONE HANDLING                      │    │
│  │ if new_status == TaskStatus.DONE:                 │    │
│  │     Triggers special completion logic              │    │
│  └────────────────────────────────────────────────────┘    │
│                         │                                    │
│                         ▼                                    │
│  ┌────────────────────────────────────────────────────┐    │
│  │ Step 3: RETRIEVE TASK                              │    │
│  │ task = self.storage.get_task(task_id)             │    │
│  └────────────────────────────────────────────────────┘    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                  STORAGE.PY - DATA LAYER                     │
│                                                              │
│  get_task(task_id):                                         │
│  - Searches internal data structure (dict/list)             │
│  - Returns Task object if found                             │
│  - Returns None if not found                                │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼ (Task object returned)
┌─────────────────────────────────────────────────────────────┐
│              BACK TO TASK_MANAGER.PY                         │
│                                                              │
│  if task:  ← Check if task was found                        │
│                                                              │
│      task.mark_as_done()  ← Call model method              │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                   MODELS.PY - DOMAIN LOGIC                   │
│                                                              │
│  Task.mark_as_done():                                       │
│                                                              │
│  ┌────────────────────────────────────────────────────┐    │
│  │ STATE CHANGE 1:                                    │    │
│  │ self.status = TaskStatus.DONE                     │    │
│  └────────────────────────────────────────────────────┘    │
│  ┌────────────────────────────────────────────────────┐    │
│  │ STATE CHANGE 2:                                    │    │
│  │ self.completed_at = datetime.now()                │    │
│  └────────────────────────────────────────────────────┘    │
│  ┌────────────────────────────────────────────────────┐    │
│  │ STATE CHANGE 3:                                    │    │
│  │ self.updated_at = self.completed_at               │    │
│  └────────────────────────────────────────────────────┘    │
│                                                              │
│  (Task object in memory is now modified)                    │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼ (Returns to task_manager.py)
┌─────────────────────────────────────────────────────────────┐
│              TASK_MANAGER.PY - PERSISTENCE                   │
│                                                              │
│      self.storage.save()  ← Persist changes                │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                  STORAGE.PY - FILE OPERATIONS                │
│                                                              │
│  save():                                                    │
│  - Serializes all Task objects to JSON                      │
│  - Writes to tasks.json file                                │
│  - Handles file I/O errors                                  │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                    FILE SYSTEM                               │
│                                                              │
│  tasks.json (persistent storage)                            │
│  - Updated with new status                                  │
│  - completed_at timestamp now present                       │
│  - updated_at timestamp refreshed                           │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                  RETURN TO USER                              │
│                                                              │
│  return True → Success!                                     │
│  CLI shows: "Task marked as complete"                       │
└─────────────────────────────────────────────────────────────┘

### State Changes During Completion

**Before Completion:**
- status: TaskStatus.TODO/IN_PROGRESS/REVIEW
- completed_at: None
- updated_at: [previous timestamp]

**Completion Trigger:**
```python
task.mark_as_done()
```

**After Completion:**
- status: TaskStatus.DONE ✓
- completed_at: [current timestamp] ✓
- updated_at: [current timestamp] ✓

### Potential Failure Points

1. **Invalid status value** → ValueError in TaskStatus(value)
2. **Task not found** → Returns None, but code doesn't handle properly (BUG!)
3. **File write permission denied** → State changes in memory but not persisted
4. **Disk full** → Corrupted JSON file
5. **Concurrent access** → Race condition, lost updates

### Persistence Mechanism

**Storage Type:** File-based JSON  
**Location:** tasks.json  
**Process:**
1. Task object modified in memory
2. storage.save() called explicitly
3. All tasks serialized to JSON
4. Written to file atomically

**Why explicit save():**
- Separation of concerns (models.py doesn't know about storage)
- Performance (batch multiple changes)
- Flexibility (easy to swap storage backend)

### Debugging Strategy

**Layer-by-layer verification:**

1. CLI input: Print task_id and status value
2. Enum conversion: Verify TaskStatus.DONE created
3. Task retrieval: Check if task object returned
4. State change: Print before/after mark_as_done()
5. Persistence: Verify tasks.json updated

**Tools:**
- Print statements at each layer
- Python debugger (pdb)
- File inspection (cat tasks.json)
- Assertions to verify state












