# CS-320 Portfolio – Contact Service & Testing

This repository contains my **Contact Service** artifact and testing work from CS-320. The project demonstrates how I design small, testable Java components and use automation (JUnit) to verify behavior against requirements. The Contact Service manages simple contact records and enforces constraints at the object boundary so invalid data never enters the system. I treat testing as part of development (“shift-left”) so that each change is covered by fast, repeatable checks in CI or my IDE.

## Artifact contents
- `Contact.java` – immutable-ID contact entity with validation  
- `ContactService.java` – in-memory CRUD service (add, update, delete, fetch)  
- `ContactTest.java` – unit tests for entity validation  
- `ContactServiceTest.java` – unit tests for service behavior and edge cases  
- *(From Project Two, if included)* `SummaryAndReflections.pdf` – brief summary and lessons learned

### Key requirements enforced
- `contactId`: non-null, length ≤ 10, unique and not editable after creation  
- `firstName` and `lastName`: non-null, length ≤ 10  
- `phone`: exactly 10 digits (numbers only)  
- `address`: non-null, length ≤ 30  

## How I ensure my code is functional and secure
I start with **requirements as tests**: each rule above has at least one positive and one negative unit test, plus boundary tests (e.g., length 10 vs. 11). I favor **fail fast validation** in constructors/setters to keep objects always-valid, and I use **meaningful exceptions** to make defects obvious. For security in a small project like this, the focus is input validation, avoiding leaking sensitive details in exception messages, and keeping dependencies minimal and up to date. In larger settings I’d add static analysis (SpotBugs), dependency checks (OWASP), and CI gates so tests and linters must pass before merge. Together, these practices keep the program functionally correct and reduce risk from bad inputs or careless changes.

## How I interpret user needs and incorporate them into a program
I translate user needs into **user stories with acceptance criteria**, then map each criterion to tests and code. For example, “As a user, I must store a 10-digit phone number” becomes tests that reject non-digits or the wrong length and code that enforces the rule. I keep a simple **traceability** from requirement → test → implementation so I can prove coverage and quickly see what breaks if a rule changes. When something is ambiguous, I document the assumption (e.g., “phone numbers are US digits only”) and design the code so that policy can evolve without rewriting everything.

## How I approach designing software
I sketch a lightweight **UML** view (entities, services, and their relationships) and aim for **single-responsibility** classes with clear invariants. I keep data private, expose only what’s needed, and prefer composition over complicated inheritance. The service owns identity and uniqueness while the entity owns validation—this separation makes unit tests small and focused. I also write tests first or alongside code so the design emerges with testability in mind, which naturally leads to smaller, cleaner methods.

## Building & running tests
- In an IDE (IntelliJ/Eclipse): right-click the `test` files and run.  
- With Maven (if you added a `pom.xml`):  
  ```bash
  mvn -q -DskipTests=false test
  ```

## What I learned
Automation isn’t just about speed; it’s about **confidence**. Clear, fast tests caught regressions immediately (for example, an attempted change that allowed 11-character names failed within seconds). Pairing validation with targeted tests gave me safer refactors and a habit of thinking about edge cases early instead of discovering them in late manual testing.

---

### Where to put this file
Place **`README.md`** at the **root of your repository** (`CS-320/README.md`). GitHub renders it automatically on the repo home page.

### Quick push steps (command line)
```bash
git add README.md
git commit -m "Add portfolio README with reflections"
git push -u origin main
```
