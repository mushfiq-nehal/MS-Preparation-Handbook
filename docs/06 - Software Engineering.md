# 📘 MSc Admission Prep — Subject 06: Software Engineering
### 🎯 JUST-Style Exam Handbook | Fast Revision Edition

> **Goal:** Visual, exam-focused revision of SE concepts — design principles, testing, SDLC models, UML, and design patterns. Every topic includes intuition, diagrams, comparisons, and exam tips.

---

## 📋 Table of Contents

| # | Topic | Tier |
|---|-------|------|
| 1 | [Cohesion & Coupling](#1-cohesion--coupling) | 🔴 Must Master |
| 2 | [Modularity](#2-modularity) | 🔴 Must Master |
| 3 | [Software Testing](#3-software-testing) | 🔴 Must Master |
| 4 | [SDLC Models](#4-sdlc-models) | 🔴 Must Master |
| 5 | [Requirements Engineering](#5-requirements-engineering) | 🔴 Must Master |
| 6 | [UML Diagrams](#6-uml-diagrams) | 🔴 Must Master |
| 7 | [Design Patterns](#7-design-patterns) | 🔴 Must Master |

---

---

# 1. Cohesion & Coupling

## 💡 Intuition First

> **Cohesion** is about how well the things INSIDE a module belong together.
> **Coupling** is about how much modules DEPEND on each other.
>
> The golden rule: **High cohesion, Low coupling** — each module does one thing well and knows as little as possible about other modules.

**Real-world analogy:**
- High cohesion = A specialist doctor (cardiologist does only heart work — focused)
- Low coupling = Departments in a company that communicate only through formal memos (not tangled in each other's work)
- Low cohesion = A "do-everything" employee who handles accounting, HR, and IT (unfocused, hard to maintain)
- High coupling = Two departments that share the same database directly (change one → breaks the other)

---

## 📐 Cohesion — Types (Worst to Best)

```
WORST ──────────────────────────────────────────► BEST

Coincidental → Logical → Temporal → Procedural → Communicational → Sequential → Functional
    1              2          3           4               5               6            7
```

| Level | Type | Description | Example |
|-------|------|-------------|---------|
| 1 (Worst) | **Coincidental** | Random, unrelated elements grouped | `utils.py` with print, sort, DB connect |
| 2 | **Logical** | Similar category but different purpose | All I/O operations in one module |
| 3 | **Temporal** | Things done at the same time | Startup initialization routines |
| 4 | **Procedural** | Steps in a procedure, order matters | Read file → parse → validate |
| 5 | **Communicational** | Work on same data | Functions that all process `user` object |
| 6 | **Sequential** | Output of one is input of next | Encrypt → compress → transmit |
| 7 (Best) | **Functional** | Single, well-defined purpose | `calculateTax()`, `sendEmail()` |

> 🔑 **Memory trick:** "**C**ats **L**ove **T**o **P**lay **C**hess **S**ometimes **F**unny" → Coincidental, Logical, Temporal, Procedural, Communicational, Sequential, Functional

---

## 📐 Coupling — Types (Worst to Best)

```
WORST ──────────────────────────────────────────► BEST

Content → Common → External → Control → Stamp → Data → Message
   1          2         3          4        5       6       7
```

| Level | Type | Description | Example |
|-------|------|-------------|---------|
| 1 (Worst) | **Content** | Module directly modifies another's internals | Module A changes Module B's variables |
| 2 | **Common** | Share global data | Both modules use global `config` variable |
| 3 | **External** | Share external format/protocol | Both depend on same file format |
| 4 | **Control** | Pass control flags | `processData(flag=true)` changes behavior |
| 5 | **Stamp** | Pass whole data structure when only part needed | Pass entire `User` object when only `name` needed |
| 6 | **Data** | Pass only needed data | `calculateTax(income, rate)` |
| 7 (Best) | **Message** | Communicate via messages/interfaces | Microservices via REST API |

> 🔑 **Memory trick:** "**C**ats **C**hase **E**very **C**urious **S**mall **D**og **M**eowing" → Content, Common, External, Control, Stamp, Data, Message

---

## ⚖️ Cohesion vs Coupling — Master Comparison

| Aspect | Cohesion | Coupling |
|--------|----------|---------|
| About | Elements WITHIN a module | BETWEEN modules |
| Goal | HIGH cohesion | LOW coupling |
| Measures | How focused a module is | How dependent modules are |
| Good sign | Module has one clear purpose | Modules are independent |
| Bad sign | Module does many unrelated things | Change in one breaks another |
| Analogy | Specialist vs generalist | Isolated vs tangled |

---

## 🔄 Why High Cohesion + Low Coupling?

```
Benefits:
  ✅ Easier to understand (each module has one job)
  ✅ Easier to test (test in isolation)
  ✅ Easier to maintain (change one module without breaking others)
  ✅ Easier to reuse (self-contained modules)
  ✅ Easier to debug (problems localized)

Bad design (low cohesion + high coupling):
  Module A ←──────────────────────────────► Module B
  (tightly tangled, change A → must change B)

Good design (high cohesion + low coupling):
  Module A ──interface──► Module B
  (communicate through well-defined interface only)
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** "High coupling is good" — NO. Low coupling is the goal.
> 🚫 **Mistake 2:** Confusing cohesion (internal) with coupling (external).
> 🚫 **Mistake 3:** Functional cohesion is the BEST, not coincidental.
> 🚫 **Mistake 4:** Data coupling is GOOD (near the best end), not bad.

---

## ⚡ One-Minute Recap

- Cohesion: how well elements within a module belong together → want HIGH
- Coupling: how much modules depend on each other → want LOW
- Best cohesion: Functional (single purpose)
- Best coupling: Data/Message (pass only needed data, use interfaces)
- Goal: each module = one job, modules = independent

---

## 📝 Probable Exam Questions

> **5-mark:** Explain cohesion and coupling with examples. Why is high cohesion and low coupling desirable?
> **Short note:** List and briefly explain the types of cohesion from worst to best.
> **Compare:** Content coupling vs Data coupling — which is better and why?
> **Identify:** Given a module description, identify its cohesion type.

---

---

# 2. Modularity

## 💡 Intuition First

> Modularity is the principle of **dividing a system into smaller, manageable, independent pieces** — like building with LEGO blocks instead of carving from one solid rock. Each block (module) can be built, tested, and replaced independently.

**Real-world analogy:** A car engine — it's made of modules (fuel system, cooling system, ignition). You can replace the cooling system without rebuilding the entire engine.

---

## 📐 What is a Module?

```
A module is a self-contained unit with:
  ✅ Well-defined interface (what it exposes)
  ✅ Hidden implementation (how it works internally)
  ✅ Single responsibility
  ✅ Minimal dependencies on other modules

Examples:
  - A function/method
  - A class
  - A package/library
  - A microservice
```

---

## 📐 Principles of Good Modular Design

### 1. Information Hiding (Encapsulation)
```
Hide internal implementation details.
Only expose what's necessary through a public interface.

Bad:  Other modules directly access internal data
Good: Other modules call methods/functions (interface)

Example:
  Bad:  user.password = "newpass"  (direct access)
  Good: user.changePassword("newpass")  (through method)
```

### 2. Separation of Concerns
```
Each module handles ONE concern/responsibility.

Bad:  UserModule handles login + email + payment + reporting
Good: AuthModule, EmailModule, PaymentModule, ReportModule
      (each handles one concern)
```

### 3. Single Responsibility Principle (SRP)
```
"A module should have one, and only one, reason to change."
— Robert C. Martin (Uncle Bob)

If a module changes for multiple reasons → split it.
```

### 4. Open/Closed Principle
```
"Open for extension, closed for modification."

Good design: Add new features by ADDING new modules,
             not by MODIFYING existing ones.
```

---

## 📊 Modular Design Metrics

```
Fan-in:  Number of modules that CALL this module
         High fan-in = module is widely reused ✅

Fan-out: Number of modules this module CALLS
         High fan-out = module is highly dependent ❌

Ideal: High fan-in, Low fan-out

         Module A
        /    |    \
       B     C     D    ← A has fan-out = 3
      / \
     E   F              ← B has fan-out = 2, E and F have fan-in = 1
```

---

## ⚖️ Modular vs Monolithic Design

| Feature | Modular | Monolithic |
|---------|---------|------------|
| Structure | Independent modules | Single large unit |
| Maintainability | Easy | Hard |
| Testing | Test in isolation | Must test whole system |
| Reusability | High | Low |
| Deployment | Independent | All-or-nothing |
| Example | Microservices | Legacy enterprise apps |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Too many tiny modules = over-modularization (overhead of managing interfaces).
> 🚫 **Mistake 2:** Modularity ≠ just splitting code into files. Modules must have clear interfaces.
> 🚫 **Mistake 3:** High fan-out is a warning sign — the module knows too much about others.

---

## ⚡ One-Minute Recap

- Modularity: divide system into independent, self-contained units
- Information hiding: expose interface, hide implementation
- SRP: one module = one reason to change
- Fan-in (callers) = high is good | Fan-out (callees) = low is good

---

## 📝 Probable Exam Questions

> **Short note:** What is modularity? What are its benefits in software design?
> **Conceptual:** Explain the principle of information hiding with an example.
> **Define:** What are fan-in and fan-out? What do high values of each indicate?

---

---

# 3. Software Testing

## 💡 Intuition First

> Testing is like **quality control in a factory** — you check the product at different stages to catch defects early. The earlier you find a bug, the cheaper it is to fix. A bug found in production costs 100x more than one found during design.

**Real-world analogy:** Building a house — you check the foundation (unit test), then each room (integration test), then the whole house (system test), then whether it meets the client's needs (acceptance test).

---

## 📐 Testing Levels

```
                    ┌─────────────────────────┐
                    │   Acceptance Testing    │  ← Does it meet user needs?
                    ├─────────────────────────┤
                    │    System Testing       │  ← Does the whole system work?
                    ├─────────────────────────┤
                    │  Integration Testing    │  ← Do modules work together?
                    ├─────────────────────────┤
                    │     Unit Testing        │  ← Does each unit work alone?
                    └─────────────────────────┘
                    (Bottom-up: start with units)
```

---

## 🔬 Unit Testing

> Test the **smallest testable unit** (function, method, class) in isolation.

```
What it tests:
  - Individual functions/methods
  - Edge cases and boundary values
  - Error handling

Example:
  Function: calculateTax(income, rate)
  Unit tests:
    ✅ calculateTax(50000, 0.2) == 10000
    ✅ calculateTax(0, 0.2) == 0        (boundary: zero income)
    ✅ calculateTax(-100, 0.2) → error  (invalid input)
    ✅ calculateTax(50000, 0) == 0      (boundary: zero rate)

Tools: JUnit (Java), pytest (Python), Jest (JavaScript)

Key principle: Tests should be FAST, ISOLATED, REPEATABLE
```

---

## 🔗 Integration Testing

> Test how **multiple modules work together**. Finds interface defects between modules.

```
Approaches:

1. Big Bang Integration:
   All modules integrated at once → test together
   Problem: Hard to isolate failures

2. Top-Down Integration:
   Start from top-level module, stub lower modules
   ┌─────────┐
   │  Main   │  ← test first
   ├────┬────┤
   │ A  │ B  │  ← stubs initially, then real modules
   └────┴────┘

3. Bottom-Up Integration:
   Start from lowest modules, use drivers for higher
   ┌────┬────┐
   │ A  │ B  │  ← test first (real modules)
   ├────┴────┤
   │  Main   │  ← driver initially, then real
   └─────────┘

4. Sandwich/Hybrid:
   Combine top-down and bottom-up
```

---

## 🖥️ System Testing

> Test the **complete, integrated system** against requirements. Black-box testing.

```
Types of system testing:
  Functional testing:    Does it do what it should?
  Performance testing:   Is it fast enough under load?
  Load testing:          How does it behave under heavy load?
  Stress testing:        What happens when pushed beyond limits?
  Security testing:      Is it secure against attacks?
  Usability testing:     Is it easy to use?
  Compatibility testing: Works on different browsers/OS?
  Recovery testing:      Does it recover from failures?
```

---

## ✅ End-to-End (E2E) Testing

> Test **complete user workflows** from start to finish, simulating real user behavior.

```
Example E2E test for e-commerce:
  1. User opens browser
  2. Navigates to product page
  3. Adds item to cart
  4. Proceeds to checkout
  5. Enters payment details
  6. Confirms order
  7. Receives confirmation email

Tests the entire stack: UI → API → Database → Email service

Tools: Selenium, Cypress, Playwright
```

---

## ⚖️ Testing Types Comparison

| Level | Scope | Who Tests | When | Finds |
|-------|-------|-----------|------|-------|
| **Unit** | Single function/class | Developer | During coding | Logic errors |
| **Integration** | Module interactions | Developer/QA | After unit tests | Interface defects |
| **System** | Whole system | QA team | After integration | System-level bugs |
| **E2E** | User workflows | QA/Automation | Before release | Workflow failures |
| **Acceptance** | Business requirements | Client/User | Before deployment | Requirement gaps |

---

## 📐 Black Box vs White Box Testing

```
Black Box Testing:
  Tester doesn't know internal code
  Tests based on INPUT → OUTPUT behavior
  Techniques: Equivalence partitioning, boundary value analysis
  Who: QA testers, clients

White Box Testing:
  Tester knows internal code structure
  Tests based on code paths, branches, conditions
  Techniques: Statement coverage, branch coverage, path coverage
  Who: Developers

Grey Box Testing:
  Partial knowledge of internals
  Combination of both approaches
```

---

## 📊 Test Coverage Metrics

```
Statement coverage: % of statements executed by tests
Branch coverage:    % of branches (if/else) covered
Path coverage:      % of all possible paths covered

Example:
  if (x > 0) {
    y = x * 2;    // Statement A
  } else {
    y = -x;       // Statement B
  }

  Test with x=5:  covers Statement A, branch "true"
  Test with x=-3: covers Statement B, branch "false"
  Both tests: 100% statement + branch coverage
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Unit testing tests ONE unit in isolation — not two modules together (that's integration).
> 🚫 **Mistake 2:** 100% code coverage ≠ bug-free software. Coverage measures what's tested, not correctness.
> 🚫 **Mistake 3:** E2E tests are slow and brittle — don't replace unit tests with E2E tests.
> 🚫 **Mistake 4:** System testing is black-box — testers don't need to know the code.

---

## 🎯 Exam Tips

> 💡 **Testing pyramid:** Many unit tests → fewer integration tests → even fewer E2E tests.
> 💡 Know the difference between verification ("are we building it right?") and validation ("are we building the right thing?").
> 💡 Regression testing: re-run tests after changes to ensure nothing broke.
> 💡 Smoke testing: quick sanity check — does the basic functionality work?

---

## ⚡ One-Minute Recap

- Unit: test one function/class in isolation
- Integration: test modules working together
- System: test complete system (black-box)
- E2E: test full user workflows
- Acceptance: test against business requirements
- Black-box: test behavior | White-box: test code paths

---

## 📝 Probable Exam Questions

> **5-mark:** Explain the different levels of software testing with examples.
> **Short note:** What is the difference between black-box and white-box testing?
> **Compare:** Unit testing vs Integration testing vs System testing.
> **Conceptual:** What is regression testing? When is it performed?

---

---

# 4. SDLC Models

## 💡 Intuition First

> SDLC (Software Development Life Cycle) is the **structured process** for building software. Different models answer the question: "In what order and how do we do requirements, design, coding, and testing?"

**Real-world analogy:** Building a house — you need a plan (requirements), blueprint (design), construction (coding), inspection (testing), and handover (deployment). Different models differ in how strictly sequential vs iterative this process is.

---

## 📐 SDLC Phases (Common to All Models)

```
1. Requirements    → What should the system do?
2. System Design   → How will it be structured?
3. Implementation  → Write the code
4. Testing         → Does it work correctly?
5. Deployment      → Release to users
6. Maintenance     → Fix bugs, add features
```

---

## 🌊 Waterfall Model

> Sequential, linear process. Each phase must be **fully completed** before the next begins. Like water flowing downhill — no going back.

```
Requirements
     │
     ▼
  Design
     │
     ▼
Implementation
     │
     ▼
  Testing
     │
     ▼
 Deployment
     │
     ▼
Maintenance
```

### Characteristics

| Feature | Detail |
|---------|--------|
| Process | Sequential, linear |
| Flexibility | Very rigid — hard to go back |
| Documentation | Heavy documentation at each phase |
| Customer involvement | Only at start and end |
| Best for | Well-defined, stable requirements |
| Worst for | Changing requirements |

### Advantages & Disadvantages

```
✅ Simple and easy to understand
✅ Well-documented phases
✅ Easy to manage (clear milestones)
✅ Works well for small, well-defined projects

❌ No working software until late in the process
❌ Cannot accommodate changing requirements
❌ Testing happens too late — bugs found late are expensive
❌ Customer sees product only at the end
```

---

## 🔄 Agile Model

> Iterative, incremental development in short **sprints** (1-4 weeks). Working software delivered frequently. Embraces change.

```
Sprint 1 (2 weeks):
  Plan → Design → Code → Test → Review
  Deliverable: Working feature set 1

Sprint 2 (2 weeks):
  Plan → Design → Code → Test → Review
  Deliverable: Working feature set 2

...repeat until product complete

Customer involved at EVERY sprint review!
```

### Agile Principles (from Agile Manifesto)

```
Individuals and interactions  > Processes and tools
Working software              > Comprehensive documentation
Customer collaboration        > Contract negotiation
Responding to change          > Following a plan
```

### Agile Frameworks

| Framework | Key Feature |
|-----------|-------------|
| **Scrum** | Sprints, daily standups, sprint reviews |
| **Kanban** | Visual board, continuous flow |
| **XP (Extreme Programming)** | Pair programming, TDD |
| **SAFe** | Scaled agile for large organizations |

### Scrum Roles & Artifacts

```
Roles:
  Product Owner: defines requirements (backlog)
  Scrum Master:  facilitates process, removes blockers
  Dev Team:      builds the product

Artifacts:
  Product Backlog: all features/requirements
  Sprint Backlog:  features for current sprint
  Increment:       working software after each sprint

Events:
  Sprint Planning → Daily Standup → Sprint Review → Retrospective
```

---

## 🌀 Spiral Model

> Combines **iterative development** with **risk analysis**. Each spiral loop = one phase. Risk is assessed and mitigated at each loop.

```
Each spiral loop has 4 quadrants:
  1. Planning:      Determine objectives, alternatives, constraints
  2. Risk Analysis: Identify and resolve risks
  3. Engineering:   Develop and test
  4. Evaluation:    Customer evaluates, plan next loop

         ┌──────────────────────────────┐
         │  Planning  │  Risk Analysis  │
         ├────────────┼─────────────────┤
         │ Evaluation │   Engineering   │
         └──────────────────────────────┘
              ↑ Each loop = one iteration
              (loops get larger as project grows)
```

### Spiral Model Characteristics

| Feature | Detail |
|---------|--------|
| Risk handling | Explicit risk analysis at each loop |
| Flexibility | High — can accommodate changes |
| Cost | High (risk analysis overhead) |
| Best for | Large, complex, high-risk projects |
| Customer involvement | At each loop evaluation |

---

## ⚖️ Waterfall vs Agile vs Spiral

| Feature | Waterfall | Agile | Spiral |
|---------|-----------|-------|--------|
| Process | Sequential | Iterative | Iterative + Risk |
| Flexibility | Low | High | High |
| Customer involvement | Start & end | Every sprint | Every loop |
| Documentation | Heavy | Light | Medium |
| Risk management | Poor | Medium | Excellent |
| Delivery | End only | Every sprint | Each loop |
| Best for | Stable requirements | Changing requirements | High-risk projects |
| Team size | Any | Small-medium | Large |

---

## 📐 Other SDLC Models

### V-Model (Verification & Validation)
```
Requirements ──────────────────────► Acceptance Testing
  System Design ──────────────────► System Testing
    Architecture Design ──────────► Integration Testing
      Module Design ──────────────► Unit Testing
                    Implementation
                    (bottom of V)

Each development phase has a corresponding test phase.
Testing planned in parallel with development.
```

### Incremental Model
```
Increment 1: Core features → deliver
Increment 2: Additional features → deliver
Increment 3: More features → deliver
...

Each increment adds functionality to the previous.
```

### Prototype Model
```
Build quick prototype → show to customer → get feedback
→ refine prototype → repeat until requirements clear
→ build final system

Good for: unclear requirements, UI-heavy systems
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Agile doesn't mean "no documentation" — it means "just enough" documentation.
> 🚫 **Mistake 2:** Waterfall is not always bad — it's appropriate for stable, well-defined projects.
> 🚫 **Mistake 3:** Spiral model is NOT just iterative — the key differentiator is **risk analysis** at each loop.
> 🚫 **Mistake 4:** Scrum is a framework, not a methodology. Agile is the methodology.

---

## 🎯 Exam Tips

> 💡 **Waterfall vs Agile** is the most common comparison question — know the table cold.
> 💡 Spiral model's key feature = **risk analysis** — always mention this.
> 💡 Agile Manifesto: 4 values and 12 principles — know the 4 values.
> 💡 V-model: each development phase maps to a testing phase (mirror image).

---

## ⚡ One-Minute Recap

- Waterfall: sequential, rigid, heavy docs, no going back
- Agile: iterative sprints, flexible, customer involved throughout
- Spiral: iterative + risk analysis at each loop, for high-risk projects
- V-model: development and testing phases mirror each other
- Scrum: sprints + product backlog + daily standups

---

## 📝 Probable Exam Questions

> **5-mark:** Compare Waterfall and Agile SDLC models. When would you choose each?
> **5-mark:** Explain the Spiral model. What is its key advantage over Waterfall?
> **Short note:** What is Scrum? Explain its roles, artifacts, and events.
> **Diagram:** Draw the Waterfall model and the V-model. Compare them.

---

---

# 5. Requirements Engineering

## 💡 Intuition First

> Requirements engineering is about **understanding what the system must do** before building it. Getting requirements wrong is the most expensive mistake in software development — you might build the wrong thing perfectly.

**Real-world analogy:** Before building a house, you ask: "How many rooms? What style? What's the budget?" These are requirements. Building without them = disaster.

---

## 📐 Functional vs Non-Functional Requirements

### Functional Requirements
> **What the system DOES** — specific behaviors, features, functions.

```
Examples:
  ✅ "The system shall allow users to register with email and password"
  ✅ "The system shall send a confirmation email after registration"
  ✅ "Users shall be able to search products by name or category"
  ✅ "The system shall generate monthly sales reports"
  ✅ "Admin shall be able to add/edit/delete products"

Format: "The system SHALL [do something]"
```

### Non-Functional Requirements (Quality Attributes)
> **How well the system does it** — quality constraints, performance, security.

```
Categories:
  Performance:    "System shall respond within 2 seconds for 95% of requests"
  Scalability:    "System shall support 10,000 concurrent users"
  Security:       "Passwords shall be stored using bcrypt hashing"
  Availability:   "System shall have 99.9% uptime"
  Usability:      "New users shall complete registration in under 3 minutes"
  Maintainability:"Code shall follow PEP8 style guide"
  Portability:    "System shall run on Windows, Linux, and macOS"
  Reliability:    "System shall recover from failure within 30 seconds"
```

---

## ⚖️ Functional vs Non-Functional

| Feature | Functional | Non-Functional |
|---------|------------|----------------|
| Describes | What system does | How well it does it |
| Testable | Yes (pass/fail) | Yes (measurable) |
| Examples | Login, search, report | Speed, security, uptime |
| Captured in | Use cases, user stories | Quality attributes |
| If missing | Feature doesn't exist | Feature works poorly |

---

## 📐 SRS (Software Requirements Specification)

> The formal document that captures all requirements. The contract between developers and stakeholders.

```
SRS Structure (IEEE 830):
  1. Introduction
     1.1 Purpose
     1.2 Scope
     1.3 Definitions, Acronyms
     1.4 References
  2. Overall Description
     2.1 Product Perspective
     2.2 Product Functions
     2.3 User Characteristics
     2.4 Constraints
  3. Specific Requirements
     3.1 Functional Requirements
     3.2 Non-Functional Requirements
     3.3 External Interface Requirements
  4. Appendices
```

### Good Requirements Properties (SMART)

```
S — Specific:    Clear and unambiguous
M — Measurable:  Can be tested/verified
A — Achievable:  Technically feasible
R — Relevant:    Necessary for the system
T — Traceable:   Can be traced to source

Bad requirement:  "The system should be fast"
Good requirement: "The system shall load the homepage in < 2 seconds
                   for 95% of requests under 1000 concurrent users"
```

---

## 📐 User Stories (Agile Requirements)

```
Format: "As a [role], I want [feature], so that [benefit]"

Examples:
  "As a customer, I want to search products by category,
   so that I can find items quickly."

  "As an admin, I want to export sales data to CSV,
   so that I can analyze it in Excel."

Acceptance criteria (Given-When-Then):
  Given: I am on the product search page
  When:  I enter "laptop" in the search box and click Search
  Then:  I see a list of laptops sorted by relevance
```

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** "The system should be user-friendly" is NOT a good non-functional requirement — not measurable.
> 🚫 **Mistake 2:** Functional requirements describe WHAT, not HOW. "Use MySQL database" is a design decision, not a requirement.
> 🚫 **Mistake 3:** Non-functional requirements are NOT optional — poor performance or security can make a system unusable.

---

## ⚡ One-Minute Recap

- Functional: what the system does (features, behaviors)
- Non-functional: how well it does it (performance, security, usability)
- SRS: formal document capturing all requirements
- Good requirements: specific, measurable, unambiguous
- User stories: "As a [role], I want [feature], so that [benefit]"

---

## 📝 Probable Exam Questions

> **5-mark:** Differentiate between functional and non-functional requirements with examples.
> **Short note:** What is an SRS? What are the properties of good requirements?
> **Write:** Write 3 functional and 3 non-functional requirements for an online banking system.
> **Identify:** Given a list of requirements, classify each as functional or non-functional.

---

---

# 6. UML Diagrams

## 💡 Intuition First

> UML (Unified Modeling Language) is the **standard visual language for software design**. Instead of writing paragraphs to describe a system, you draw diagrams. Different diagrams show different views of the system.

**Real-world analogy:** Architectural blueprints — floor plan (structure), electrical diagram (behavior), plumbing diagram (flow). Each shows a different aspect of the same building.

---

## 📐 UML Diagram Types

```
UML Diagrams
├── Structural (static view)
│   ├── Class Diagram          ← most important
│   ├── Object Diagram
│   ├── Component Diagram
│   └── Deployment Diagram
│
└── Behavioral (dynamic view)
    ├── Use Case Diagram        ← most important
    ├── Sequence Diagram        ← most important
    ├── Activity Diagram
    ├── State Machine Diagram
    └── Collaboration Diagram
```

---

## 👤 Use Case Diagram

> Shows **what the system does** from the user's perspective. Captures functional requirements visually.

```
Elements:
  Actor:    Stick figure (user or external system)
  Use Case: Oval (a function/feature)
  System:   Rectangle boundary
  Relationships:
    Association: Actor ──── Use Case
    Include:     Use Case ──«include»──► Use Case (always happens)
    Extend:      Use Case ──«extend»──► Use Case (sometimes happens)
    Generalization: Child ──────────► Parent

Example: Online Shopping System

┌─────────────────────────────────────────────┐
│              Online Shopping System          │
│                                             │
│  (Browse Products)    (Search Products)     │
│                                             │
│  (Add to Cart) ──«include»──► (View Cart)   │
│                                             │
│  (Checkout) ──«include»──► (Make Payment)   │
│                                             │
│  (Track Order) ──«extend»──► (Cancel Order) │
│                                             │
└─────────────────────────────────────────────┘
     │                              │
  Customer                        Admin
  (Actor)                        (Actor)
```

---

## 📦 Class Diagram

> Shows the **static structure** of the system — classes, attributes, methods, and relationships.

```
Class notation:
┌─────────────────┐
│   ClassName     │  ← Class name
├─────────────────┤
│ - attribute: type│  ← Attributes (- private, + public, # protected)
├─────────────────┤
│ + method(): type│  ← Methods
└─────────────────┘

Example:
┌──────────────────┐         ┌──────────────────┐
│     Customer     │         │      Order       │
├──────────────────┤         ├──────────────────┤
│ - id: int        │         │ - orderId: int   │
│ - name: String   │  1   *  │ - date: Date     │
│ - email: String  │─────────│ - total: double  │
├──────────────────┤ places  ├──────────────────┤
│ + login()        │         │ + getTotal()     │
│ + register()     │         │ + addItem()      │
└──────────────────┘         └──────────────────┘
                                      │ contains
                                      │ 1..*
                              ┌───────────────────┐
                              │     OrderItem     │
                              ├───────────────────┤
                              │ - productId: int  │
                              │ - quantity: int   │
                              │ - price: double   │
                              └───────────────────┘
```

### Class Relationships

| Relationship | Symbol | Meaning | Example |
|-------------|--------|---------|---------|
| **Association** | ──── | General relationship | Customer places Order |
| **Aggregation** | ──◇ | "Has-a" (weak) | Department has Employees |
| **Composition** | ──◆ | "Has-a" (strong, lifecycle) | House has Rooms |
| **Inheritance** | ──▷ | "Is-a" | Dog is-a Animal |
| **Realization** | ──▷ (dashed) | Implements interface | Dog implements Runnable |
| **Dependency** | ──► (dashed) | Uses temporarily | Order uses TaxCalculator |

### Multiplicity Notation

```
1      → exactly one
0..1   → zero or one (optional)
*      → zero or more
1..*   → one or more
2..5   → between 2 and 5
```

---

## 🔄 Sequence Diagram

> Shows **how objects interact over time** — the sequence of messages exchanged.

```
Elements:
  Lifeline:    Vertical dashed line (object's life)
  Activation:  Rectangle on lifeline (object is active)
  Message:     Horizontal arrow (method call)
  Return:      Dashed arrow (return value)

Example: User Login Sequence

User        Browser      AuthController    Database
 │             │               │               │
 │──login()──►│               │               │
 │             │──POST /login─►│               │
 │             │               │──findUser()──►│
 │             │               │◄──user data───│
 │             │               │──verifyPwd()  │
 │             │               │               │
 │             │◄──200 OK──────│               │
 │◄──redirect─│               │               │
 │             │               │               │
```

---

## ⚖️ Use Case vs Class vs Sequence Diagram

| Diagram | Shows | When Used | Audience |
|---------|-------|-----------|---------|
| **Use Case** | What system does | Requirements phase | Client, stakeholders |
| **Class** | System structure | Design phase | Developers |
| **Sequence** | Object interactions | Design/implementation | Developers |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Use case actors can be external systems, not just humans.
> 🚫 **Mistake 2:** `«include»` = always happens (mandatory). `«extend»` = sometimes happens (optional).
> 🚫 **Mistake 3:** Composition (◆) = child cannot exist without parent. Aggregation (◇) = child can exist independently.
> 🚫 **Mistake 4:** In sequence diagrams, time flows downward — earlier messages are higher.

---

## 🎯 Exam Tips

> 💡 **Use case diagram:** Draw actors outside the system boundary, use cases inside.
> 💡 **Class diagram:** Show multiplicity on both ends of associations.
> 💡 **Sequence diagram:** Show activation boxes when an object is processing.
> 💡 Include vs Extend: "Login includes Validate Credentials" | "Checkout extends Apply Coupon"

---

## ⚡ One-Minute Recap

- Use case: actors + use cases + system boundary (what system does)
- Class: classes + attributes + methods + relationships (structure)
- Sequence: objects + messages + time (how they interact)
- Include: mandatory sub-use case | Extend: optional sub-use case
- Composition: strong ownership | Aggregation: weak ownership

---

## 📝 Probable Exam Questions

> **5-mark:** Draw a use case diagram for an ATM system. Include at least 4 use cases and 2 actors.
> **5-mark:** Draw a class diagram for a library management system with at least 3 classes and their relationships.
> **5-mark:** Draw a sequence diagram for the "Place Order" use case in an e-commerce system.
> **Short note:** What is the difference between include and extend relationships in use case diagrams?

---

---

# 7. Design Patterns

## 💡 Intuition First

> Design patterns are **proven, reusable solutions to common software design problems**. They're not code — they're templates. Like architectural blueprints: "When you need a door, here's the standard way to design one."

**Real-world analogy:** Recipes in a cookbook. You don't invent a new way to bake bread every time — you follow a proven recipe and adapt it to your needs.

**Why they matter:** Patterns give developers a shared vocabulary. "Use a Singleton here" communicates a complete design decision in one word.

---

## 📐 Pattern Categories (Gang of Four)

```
Design Patterns
├── Creational (how objects are created)
│   ├── Singleton
│   ├── Factory Method
│   ├── Abstract Factory
│   ├── Builder
│   └── Prototype
│
├── Structural (how objects are composed)
│   ├── Adapter
│   ├── Decorator
│   ├── Facade
│   ├── Proxy
│   └── Composite
│
└── Behavioral (how objects communicate)
    ├── Observer
    ├── Strategy
    ├── Command
    ├── Iterator
    └── Template Method
```

---

## 🔒 Singleton Pattern

> **Ensure a class has only ONE instance** and provide a global access point to it.

```
Problem: You need exactly one database connection, one config manager,
         one logger — creating multiple would waste resources or cause conflicts.

Solution: Make constructor private, provide static getInstance() method.

class DatabaseConnection {
    private static instance = null;

    private DatabaseConnection() {
        // private constructor — can't call new DatabaseConnection()
    }

    public static getInstance() {
        if (instance == null) {
            instance = new DatabaseConnection();
        }
        return instance;
    }

    public query(sql) { ... }
}

// Usage:
db1 = DatabaseConnection.getInstance();
db2 = DatabaseConnection.getInstance();
// db1 == db2 (same object!)
```

### Singleton Structure

```
┌─────────────────────────────────┐
│         DatabaseConnection      │
├─────────────────────────────────┤
│ - instance: DatabaseConnection  │  ← static, private
├─────────────────────────────────┤
│ - DatabaseConnection()          │  ← private constructor
│ + getInstance(): DBConnection   │  ← static, public
│ + query(sql): ResultSet         │
└─────────────────────────────────┘
```

### When to Use Singleton

```
✅ Database connection pool
✅ Configuration manager
✅ Logger
✅ Thread pool
✅ Cache

⚠️ Overuse is an anti-pattern — makes testing hard (global state)
```

---

## 🏭 Factory Method Pattern

> **Define an interface for creating objects, but let subclasses decide which class to instantiate.** Decouple object creation from usage.

```
Problem: You need to create different types of objects (Circle, Rectangle, Triangle)
         but the client code shouldn't know which concrete class to instantiate.

Solution: Define a factory method that subclasses override.

// Abstract creator
abstract class ShapeFactory {
    abstract createShape(): Shape;  // factory method

    drawShape() {
        shape = createShape();      // uses factory method
        shape.draw();
    }
}

// Concrete creators
class CircleFactory extends ShapeFactory {
    createShape(): Shape {
        return new Circle();
    }
}

class RectangleFactory extends ShapeFactory {
    createShape(): Shape {
        return new Rectangle();
    }
}

// Usage:
factory = new CircleFactory();
factory.drawShape();  // draws a circle
```

### Factory Pattern Structure

```
┌──────────────┐         ┌──────────────┐
│  ShapeFactory│         │    Shape     │
│  (abstract)  │         │  (interface) │
├──────────────┤         ├──────────────┤
│+createShape()│         │ + draw()     │
│+drawShape()  │         └──────┬───────┘
└──────┬───────┘                │
       │                   ┌────┴────┐
  ┌────┴────┐           Circle  Rectangle
  │         │
CircleFactory RectangleFactory
```

### Simple Factory vs Factory Method vs Abstract Factory

| Pattern | Creates | Flexibility |
|---------|---------|-------------|
| Simple Factory | One factory, multiple products | Low |
| Factory Method | Subclass decides product | Medium |
| Abstract Factory | Family of related products | High |

---

## 👁️ Observer Pattern

> **Define a one-to-many dependency** so that when one object (Subject) changes state, all its dependents (Observers) are notified automatically.

```
Problem: Multiple parts of a system need to react when data changes.
         E.g., when stock price changes → update chart, alert, portfolio.

Solution: Subject maintains a list of observers and notifies them on change.

interface Observer {
    update(data): void;
}

class StockMarket {  // Subject
    private observers = [];
    private price;

    subscribe(observer) {
        observers.add(observer);
    }

    unsubscribe(observer) {
        observers.remove(observer);
    }

    setPrice(newPrice) {
        price = newPrice;
        notifyAll();
    }

    notifyAll() {
        for each observer in observers:
            observer.update(price);
    }
}

class PriceChart implements Observer {
    update(price) { redrawChart(price); }
}

class PriceAlert implements Observer {
    update(price) {
        if (price > threshold) sendAlert();
    }
}

// Usage:
market = new StockMarket();
market.subscribe(new PriceChart());
market.subscribe(new PriceAlert());
market.setPrice(150);  // both chart and alert updated!
```

### Observer Structure

```
┌──────────────────┐         ┌──────────────┐
│   StockMarket    │         │   Observer   │
│   (Subject)      │         │  (interface) │
├──────────────────┤  1   *  ├──────────────┤
│ - observers[]    │─────────│ + update()   │
├──────────────────┤         └──────┬───────┘
│ + subscribe()    │                │
│ + unsubscribe()  │         ┌──────┴──────┐
│ + notifyAll()    │      PriceChart   PriceAlert
│ + setPrice()     │
└──────────────────┘
```

### Real-World Observer Examples

```
✅ Event listeners in JavaScript (addEventListener)
✅ MVC pattern (Model notifies View)
✅ Pub/Sub messaging systems (Kafka, RabbitMQ)
✅ React state management (Redux)
✅ Database triggers
✅ News subscription services
```

---

## ⚖️ Design Patterns Comparison

| Pattern | Category | Problem Solved | Key Mechanism |
|---------|----------|----------------|---------------|
| **Singleton** | Creational | One instance only | Private constructor + static instance |
| **Factory** | Creational | Decouple creation from use | Factory method / subclass decides |
| **Observer** | Behavioral | Notify multiple dependents | Subscribe/notify mechanism |
| **Strategy** | Behavioral | Swap algorithms at runtime | Interface + multiple implementations |
| **Decorator** | Structural | Add behavior without subclassing | Wrap object with decorator |
| **Adapter** | Structural | Make incompatible interfaces work | Wrapper that translates calls |

---

## ⚠️ Common Mistakes

> 🚫 **Mistake 1:** Singleton is NOT always good — it creates global state, making testing hard.
> 🚫 **Mistake 2:** Factory Method ≠ Simple Factory. Factory Method uses inheritance; Simple Factory uses a single class.
> 🚫 **Mistake 3:** Observer pattern: Subject doesn't know what observers DO — it just calls `update()`.
> 🚫 **Mistake 4:** Design patterns are solutions to RECURRING problems — don't force them where they don't fit.

---

## 🎯 Exam Tips

> 💡 **Singleton:** Know the private constructor + static getInstance() pattern cold.
> 💡 **Factory:** "Decouple object creation from usage" — this phrase defines it.
> 💡 **Observer:** "One-to-many dependency" — Subject notifies all Observers.
> 💡 Always draw the UML class diagram when explaining a pattern.

---

## ⚡ One-Minute Recap

- Singleton: one instance, private constructor, static getInstance()
- Factory: decouple creation, subclass decides which object to create
- Observer: subject notifies all subscribed observers on state change
- Creational: how objects created | Structural: how composed | Behavioral: how communicate

---

## 📝 Probable Exam Questions

> **5-mark:** Explain the Singleton design pattern with a UML diagram and code example.
> **5-mark:** Explain the Observer pattern. Give a real-world example and draw the class diagram.
> **Short note:** What is the Factory Method pattern? How does it differ from Simple Factory?
> **Compare:** Singleton vs Factory vs Observer — category, problem, and solution.

---

---

# 🏁 Master Quick Revision Sheet — Software Engineering

## ⚡ Cohesion & Coupling Cheat Sheet

```
COHESION (want HIGH):
Worst → Best:
Coincidental → Logical → Temporal → Procedural →
Communicational → Sequential → Functional

COUPLING (want LOW):
Worst → Best:
Content → Common → External → Control →
Stamp → Data → Message
```

## 🔑 Key Facts to Remember

| Fact | Detail |
|------|--------|
| Best cohesion | Functional (single purpose) |
| Best coupling | Data / Message |
| Waterfall | Sequential, rigid, heavy docs |
| Agile | Iterative sprints, flexible, customer involved |
| Spiral | Iterative + risk analysis at each loop |
| V-model | Dev phases mirror test phases |
| Functional req | What system does |
| Non-functional req | How well it does it |
| Include (UML) | Mandatory sub-use case |
| Extend (UML) | Optional sub-use case |
| Composition | Strong ownership (child dies with parent) |
| Aggregation | Weak ownership (child can exist alone) |
| Singleton | One instance, private constructor |
| Factory | Decouple creation from usage |
| Observer | One-to-many notification |

## 🧠 Memory Tricks

- **Cohesion types:** "**C**ats **L**ove **T**o **P**lay **C**hess **S**ometimes **F**unny"
- **Coupling types:** "**C**ats **C**hase **E**very **C**urious **S**mall **D**og **M**eowing"
- **SDLC models:** "**W**ater **A**lways **S**pirals **V**ertically **I**n **P**ipes" → Waterfall, Agile, Spiral, V-model, Incremental, Prototype
- **UML diagrams:** "**U**se **C**lass **S**equence" → the 3 most important
- **Design pattern categories:** "**C**reate **S**tructure **B**ehavior" → Creational, Structural, Behavioral

## 🎯 Top 10 Most Probable Exam Questions

1. Explain cohesion and coupling with types and examples
2. Compare Waterfall vs Agile SDLC models
3. Explain the Spiral model — what makes it unique?
4. Differentiate functional vs non-functional requirements with examples
5. Draw a use case diagram for a given system
6. Draw a class diagram with relationships and multiplicity
7. Draw a sequence diagram for a given scenario
8. Explain Singleton pattern with code and UML
9. Explain Observer pattern with real-world example
10. Compare unit testing, integration testing, and system testing

## 📊 SDLC Quick Reference

```
┌──────────────┬────────────┬──────────┬──────────────┬──────────────┐
│ Model        │ Process    │ Flexible?│ Risk Mgmt    │ Best For     │
├──────────────┼────────────┼──────────┼──────────────┼──────────────┤
│ Waterfall    │ Sequential │ Low      │ Poor         │ Stable reqs  │
│ Agile/Scrum  │ Iterative  │ High     │ Medium       │ Changing reqs│
│ Spiral       │ Iterative  │ High     │ Excellent    │ High-risk    │
│ V-Model      │ Sequential │ Low      │ Good         │ Safety-crit  │
│ Incremental  │ Incremental│ Medium   │ Medium       │ Large systems│
│ Prototype    │ Iterative  │ High     │ Medium       │ Unclear reqs │
└──────────────┴────────────┴──────────┴──────────────┴──────────────┘
```

---

> 📌 **End of Subject 06: Software Engineering**
>
> Next: **Subject 07 — Database Management System (DBMS)** →

---

*Handbook generated for MSc Admission Preparation | JUST-Style Exam Focus*
*Version 1.0 | Software Engineering*
