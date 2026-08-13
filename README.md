# SudoGrid

> 🧩 A zero-setup, offline Sudoku desktop application built with Java Swing, featuring an interactive 9×9 board, digit selection, move validation, solution reveal, reset, and exit controls.

**Java 20 · Java Swing · AWT · NetBeans GUI Builder · Apache Maven**

---

## 1. 🎯 Project Overview

SudoGrid is a Java desktop Sudoku application built with Swing, where a 9×9 grid of interactive buttons acts as the playable board. Players select a digit, place it into open cells, validate their entries against the stored answer key, and reveal or hide the complete solution when needed.

The application is designed as a simple offline Sudoku experience with no account, network connection, database, or external services. All game state remains in memory and the application runs entirely on the local machine.

> 📝 **Scope:** SudoGrid currently ships with one fixed Sudoku puzzle and a stored answer key. It does not contain a Sudoku generator or backtracking solver — the Solution feature reveals the stored answer, while Check Moves compares user entries against that answer key.

---

## 2. ✨ Features

### 🔢 Digit-first Input

- Select a digit from `1–9` using the selector bar.
- The currently selected digit is highlighted in blue.
- Other digits remain black, making the active input mode visible.

### 🧩 Interactive 9×9 Sudoku Board

- Every Sudoku cell is represented by an interactive `JButton`.
- Clicking an editable cell places the currently selected digit.
- The board contains **35 prefilled clue cells**.

### 🔒 Protected Clue Cells

- Prefilled puzzle cells cannot be overwritten.
- Clicking a clue cell displays an information dialog instead of changing its value.

### ✅ Move Validation

- **Check Moves** compares user-entered values against the stored answer key.
- Incorrect entries are highlighted in red.
- The button changes to **Remove Checks** while validation highlighting is active.
- Removing checks clears the highlighting and restores the board state.

### 💡 Solution Reveal

- **Solution** fills all non-clue cells with the stored correct values.
- The button changes to **Hide Solution**.
- Hiding the solution clears the non-clue cells again.

### 🔄 Reset

- Clears all user-entered values.
- Preserves the original clue cells.
- Requires confirmation before resetting the board.

### 🚪 Exit

- Closes the application after confirmation.

### 🎨 Nimbus Look & Feel

- Attempts to use Java's Nimbus look-and-feel at startup.
- Falls back to the platform default if Nimbus is unavailable.

---

## 3. 🛠️ Tech Stack

| Technology | Layer | Responsibility & Why |
|---|---|---|
| **Java 20** | Language / Runtime | Powers the complete application. Maven is configured with Java 20 as the source and target version. |
| **Java Swing (`javax.swing`)** | UI | Renders the main window, 9×9 Sudoku board, digit selector, control buttons, and confirmation/information dialogs. |
| **AWT (`java.awt`)** | Events / Rendering | Handles `ActionListener`, `ActionEvent`, `EventQueue.invokeLater`, and UI colors. |
| **NetBeans GUI Builder** | UI Authoring | Uses `sudokoFile.form` to define the interface and generate the Swing `GroupLayout` configuration. |
| **Apache Maven** | Build / Packaging | Compiles the project and packages the application as a JAR artifact. |
| **exec-maven-plugin** | Execution | Provides Maven-based execution configuration for the Java application. |

### 📦 Dependency Profile

SudoGrid intentionally has **zero third-party runtime dependencies**.

There is:

- ❌ No web framework
- ❌ No database
- ❌ No backend server
- ❌ No external API
- ❌ No authentication system
- ❌ No environment configuration

The JDK and Maven are sufficient to build and run the application.

---

## 4. 🏗️ Architecture

~~~mermaid
flowchart TD
    A["JVM Startup<br/>main()"] --> B["Nimbus Look & Feel"]
    B --> C["EventQueue.invokeLater"]
    C --> D["sudokoFile JFrame"]

    D --> E["Digit Selector<br/>1 - 9"]
    D --> F["9×9 Sudoku Grid<br/>81 JButtons"]
    D --> G["Control Bar<br/>Check · Solution · Reset · Exit"]

    E --> H["Swing Event Handlers"]
    F --> H
    G --> H

    H --> I["AssignTurn()"]
    H --> J["ResetGame()"]
    H --> K["SeeSolution()"]
    H --> L["CheckMoves()"]

    I --> M["In-Memory Game State"]
    J --> M
    K --> M
    L --> M

    M --> N["turn"]
    M --> O["globalFlag"]
    M --> P["solvedBoard"]
    M --> Q["predefinedBtns"]

    N --> R["UI Update"]
    O --> R
    P --> R
    Q --> R

    R --> F
~~~

### 🔄 How Responsibilities Are Split

- **JVM startup** executes `main()` and attempts to install the Nimbus look-and-feel.
- **EventQueue** launches the Swing interface on the AWT Event Dispatch Thread.
- **`sudokoFile`** extends `JFrame` and contains the application's UI, game state, and event-handling logic.
- **The 9×9 grid** consists of 81 `JButton` cells whose text and background colors represent the current board state.
- **Digit and control actions** are handled through Swing event handlers such as `AssignTurn()`, `ResetGame()`, `SeeSolution()`, and `CheckMoves()`.
- **Game state remains entirely in memory** through variables such as `turn`, `globalFlag`, `solvedBoard`, and `predefinedBtns`.
- **There are no external communication layers** — no filesystem persistence, network requests, database, authentication, or third-party services.

### 🧠 State Model

SudoGrid does not use a separate model class.

Instead:

~~~text
Cell value   → JButton text
Cell state   → JButton background color
Solution     → solvedBoard
Clue cells   → predefinedBtns
Active digit → turn
Toggle state → globalFlag
~~~

This keeps the application simple, but also tightly couples the game logic to the Swing UI.

---

## 5. 📁 Project Structure

~~~text
SUDOGRID/
├── .github/
│   └── modernize/
│       └── java-upgrade/
│           └── hooks/
│               └── scripts/
│                   ├── recordToolUse.ps1
│                   └── recordToolUse.sh
│
└── Sudoku_project/
    ├── .gitignore
    ├── README.md
    └── sudoko_project/
        ├── pom.xml
        ├── nbactions.xml
        ├── src/
        │   └── main/
        │       └── java/
        │           └── com/
        │               └── mycompany/
        │                   └── sudoko_project/
        │                       ├── sudokoFile.java
        │                       └── sudokoFile.form
        ├── target/
        └── sudoko_project-1.0-SNAPSHOT.jar.jar
~~~

### 📌 Important Files

| Path | Why It Matters |
|---|---|
| `sudoko_project/src/main/java/.../sudokoFile.java` | Main application class containing the `JFrame`, generated UI code, 81 cell handlers, digit handlers, control handlers, answer key, and `main()`. |
| `sudoko_project/src/main/java/.../sudokoFile.form` | NetBeans GUI Builder XML layout descriptor used to define the application's interface. |
| `sudoko_project/pom.xml` | Maven build definition, Java 20 source/target configuration, JAR packaging, and project coordinates. |
| `sudoko_project/nbactions.xml` | NetBeans Run/Debug/Profile configuration. |
| `Sudoku_project/README.md` | Original project documentation. |
| `sudoko_project/target/` | Generated Maven build output. |
| `sudoko_project-1.0-SNAPSHOT.jar.jar` | Existing committed build artifact. |

> ⚠️ **Note:** `sudokoFile.java` contains approximately 2,190 lines and combines the application's UI, state, and logic.

---

## 6. ⚙️ Installation & Setup

### 📋 Prerequisites

| Requirement | Purpose |
|---|---|
| **JDK 20 or newer** | Required because the Maven compiler is configured for Java 20. |
| **Apache Maven 3.6+** | Required to build and run the project through Maven. |
| **Git** | Required to clone the repository. |
| **Apache NetBeans** | Optional; useful for editing the GUI through `sudokoFile.form`. |

No database, API key, external service account, or environment variable is required.

### 📥 Clone

~~~bash
git clone https://github.com/Ayushjungari/SUDOGRID.git
cd SUDOGRID/Sudoku_project/sudoko_project
~~~

### 📦 Build

~~~bash
mvn clean package
~~~

### ▶️ Run Locally

Use Maven with the actual main class:

~~~bash
mvn exec:java -Dexec.mainClass=com.mycompany.sudoko_project.sudokoFile
~~~

Alternatively, run the compiled classes directly:

~~~bash
java -cp target/classes com.mycompany.sudoko_project.sudokoFile
~~~

### ⚠️ Maven Configuration Note

The current `pom.xml` contains an `exec.mainClass` value pointing to:

~~~text
com.mycompany.sudoko_project.Sudoko_project
~~~

That class does not exist in the source tree.

The actual application entry point is:

~~~text
com.mycompany.sudoko_project.sudokoFile
~~~

Therefore, explicitly passing the main class as shown above is recommended unless the Maven configuration is corrected.

### 🔐 Environment Variables

None.

SudoGrid does not require:

- `.env`
- `.env.example`
- API credentials
- Secret keys
- Runtime configuration

### 🗄️ Database

None.

All application state is maintained in memory and nothing is persisted between runs.

### 📦 Build Artifact

Running:

~~~bash
mvn clean package
~~~

produces:

~~~text
target/sudoko_project-1.0-SNAPSHOT.jar
~~~

The current Maven configuration does not add an executable JAR manifest or shade/assembly configuration, so the artifact is not directly runnable using:

~~~bash
java -jar ...
~~~

Use the classpath command instead, or configure Maven with an appropriate packaging plugin.

---

## 7. 🚀 Usage

1. ▶️ Launch the application. The Sudoku window opens with the fixed puzzle and its **35 prefilled clue cells**.
2. 🔢 Click a digit from `1–9` in the selector bar. The selected digit turns blue.
3. 🧩 Click an empty cell to place the selected digit.
4. 🔒 Clicking a prefilled clue cell displays an information dialog and leaves the clue unchanged.
5. 🔄 Change the selected digit at any time and continue filling the board.
6. ✅ Click **Check Moves** to compare entered values against the stored answer key.
7. 🔴 Incorrect entries are highlighted in red. Click **Remove Checks** to clear the validation state.
8. 💡 Click **Solution** to reveal the stored solution.
9. 🙈 Click **Hide Solution** to clear the revealed non-clue cells.
10. 🔄 Click **Reset** and confirm to clear user entries while preserving the original clues.
11. 🚪 Click **Exit** and confirm to close the application.

---

## 8. 🔌 API Documentation

SudoGrid does **not** expose a backend API.

There is:

- ❌ No HTTP server
- ❌ No REST API
- ❌ No GraphQL API
- ❌ No client/server communication
- ❌ No external service calls

All application interaction happens in-process through Swing event handlers.

### 🧠 Internal Application Operations

| Method | Trigger | Purpose |
|---|---|---|
| `AssignTurn(JButton)` | Digit selector buttons | Resets selector backgrounds, highlights the selected digit in blue, and stores the digit in `turn`. |
| `r{row}c{col}ActionPerformed(...)` | Sudoku grid cells | Writes the selected digit into open cells; clue cells display the protected-cell dialog. |
| `ResetGame()` | Reset button | Clears user-entered values and restores default cell colors while preserving clue cells. |
| `SeeSolution()` | Solution / Hide Solution | Toggles the stored solution into non-clue cells or clears those cells. |
| `CheckMoves()` | Check Moves / Remove Checks | Compares non-empty cells against `solvedBoard` and highlights incorrect entries in red. |
| `main(String[])` | JVM startup | Installs Nimbus look-and-feel and launches the Swing frame on the Event Dispatch Thread. |

---

## 9. 🧠 Engineering Decisions

### 🖥️ Swing Desktop Application Instead of a Web Application

**Decision:** Build SudoGrid as a Java Swing desktop application.

**Why:** The intended experience is an offline Sudoku board with no accounts, network communication, or data synchronization. Swing ships with the JDK, allowing the complete application to remain dependency-free.

**Trade-off:** No browser or mobile accessibility, and Swing has a more dated visual language compared with modern web UI frameworks.

### 🎨 NetBeans GUI Builder + GroupLayout

**Decision:** Use the NetBeans GUI Builder and generated `GroupLayout` configuration.

**Why:** The interface contains a large number of UI components and a rigid 9×9 grid. A form editor provides reproducible positioning without manually maintaining every layout constraint.

**Trade-off:** `initComponents()` is generated code and should not be edited manually. UI changes can produce large, difficult-to-review diffs.

### 🧱 Single Class for View, Controller, and State

**Decision:** Keep the application inside the `sudokoFile` JFrame.

**Why:** For a small single-screen application, this keeps UI events, state, and rendering close together.

**Trade-off:** `sudokoFile.java` is approximately 2,190 lines and lacks separation of concerns, making future features harder to implement and test.

### 🧩 Board State Stored Directly in UI Widgets

**Decision:** Use the Swing buttons themselves as the source of truth for board state.

**Why:** A cell's value is represented by its button text and its visual state by its background color. This eliminates synchronization between a separate model and the UI.

**Trade-off:** Sudoku logic becomes tightly coupled to Swing components and cannot be easily tested independently from the UI.

### 💡 Stored Answer Key Instead of a Solver

**Decision:** Store a fixed `solvedBoard` rather than implementing a Sudoku solver or generator.

**Why:** It provides a deterministic play → validate → reveal workflow without introducing solver complexity.

**Trade-off:** The application contains only one puzzle and one difficulty. It also validates against the stored answer rather than checking whether a user's board satisfies Sudoku's row, column, and 3×3 subgrid constraints.

### 🔢 Generated Per-Cell Event Handlers

**Decision:** Use individual generated handlers for the 81 grid cells.

**Why:** This follows the NetBeans GUI Builder's event wiring and allows clue cells to have their own protected-cell behaviour.

**Trade-off:** There are 81 near-identical handlers, making future behaviour changes repetitive.

### 🎨 Nimbus Look & Feel with Fallback

**Decision:** Attempt to use Nimbus and fall back to the platform default.

**Why:** Provides a consistent appearance without adding a third-party UI theming dependency.

**Trade-off:** Appearance can still vary across environments where Nimbus is unavailable.

### 🔒 No Dependencies, Configuration, or Persistence

**Decision:** Keep the application completely local and dependency-free.

**Why:** This makes the project reproducible on a JDK 20 machine and eliminates the need to manage credentials, network access, database connections, or persistent user data.

**Trade-off:** Nothing survives application restart, and features such as saved progress, scores, or puzzle libraries would require a storage layer in the future.

---

## 10. 🧪 Testing

SudoGrid currently has **no automated test suite**.

There is:

- No `src/test` directory
- No testing framework declared in `pom.xml`
- No test script
- No CI workflow

### ✅ Manual Verification

The implemented behaviour can be manually verified using the following workflow:

| # | Test | Expected Result |
|---|---|---|
| 1 | Launch the application | Window opens with 35 clue cells filled and other cells empty. |
| 2 | Select digit `5` | `5` turns blue while other digits remain black. |
| 3 | Click an empty cell | Cell displays `5` on a white background. |
| 4 | Click a clue cell | Protected-cell dialog appears and clue remains unchanged. |
| 5 | Enter correct + incorrect values and click **Check Moves** | Incorrect cells turn red and the button changes to **Remove Checks**. |
| 6 | Click **Remove Checks** | Highlighting is cleared and the button returns to **Check Moves**. |
| 7 | Click **Solution** | All non-clue cells are filled with the stored solution. |
| 8 | Click **Hide Solution** | Non-clue cells are cleared. |
| 9 | Enter values → click **Reset** → confirm | User entries are cleared while clues remain intact. |
| 10 | Click **Exit** → confirm | Application closes. |

---

## 11. 🚧 Limitations & Future Improvements

### ⚠️ Current Limitations

- 🧩 **One hardcoded puzzle:** The board and answer key are literal arrays in the source. There is no puzzle generator, puzzle library, or difficulty selection.
- 🧠 **No solving algorithm:** The Solution feature reveals a stored answer key instead of calculating a solution.
- 📏 **Validation is not rule-based:** Row, column, and 3×3 subgrid constraints are not evaluated. Correctness is determined by comparison with the stored answer key.
- ⚠️ **String comparison issue:** `CheckMoves()` uses `!=` for string comparison instead of `.equals()`. It currently works for interned literals but is technically fragile.
- ⚠️ **Confirmation dialog issue:** Reset and Exit compare the result of `showConfirmDialog()` against `JOptionPane.YES_NO_OPTION` instead of `YES_OPTION`.
- 🧱 **Monolithic implementation:** Approximately 2,190 lines are contained in a single class with 81 duplicated cell handlers.
- ↩️ **No undo/redo:** User actions cannot be reversed.
- ⏱️ **No timer:** There is no gameplay timer.
- 🏆 **No scoring:** The application does not track score or performance.
- 💡 **No hints:** There is no hint system.
- 🏁 **No win detection:** The application does not automatically detect puzzle completion.
- 💾 **No persistence:** Progress is lost when the application exits.
- 📦 **Committed build output:** `target/` and the generated JAR are currently tracked in version control.
- ⚙️ **Non-launchable packaged JAR:** The current JAR does not contain the required executable manifest configuration.
- ⚠️ **Maven execution configuration:** `pom.xml` points `exec.mainClass` to a class that does not exist.
- 🧪 **No automated tests or CI:** The repository currently relies on manual verification.

### 🚀 Future Improvements

| Priority | Improvement |
|---|---|
| **High** | 🧱 Extract a dedicated `SudokuBoard` model containing board state and Sudoku rule validation. |
| **High** | 🧠 Implement a backtracking Sudoku solver and puzzle generator. |
| **High** | 🧩 Support multiple puzzles and difficulty levels. |
| **High** | 🔢 Replace the 81 generated cell handlers with a shared `ActionListener` and a 2D cell structure. |
| **High** | 🐛 Fix string comparison using `.equals()` and correct confirmation-dialog handling with `JOptionPane.YES_OPTION`. |
| **Medium** | ✅ Add real-time row, column, and 3×3 constraint validation. |
| **Medium** | 🏆 Add win detection, scoring, move counter, and timer. |
| **Medium** | 💡 Add hints and undo/redo functionality. |
| **Medium** | 💾 Add save/resume functionality using local storage. |
| **Medium** | 🧪 Extract the Sudoku model and add JUnit 5 tests for rules, solving, reset, and solution transitions. |
| **Medium** | 🔄 Add GitHub Actions CI running `mvn verify` on every push. |
| **Low** | 📦 Configure Maven to produce a directly launchable JAR or native installer using `jpackage`. |
| **Low** | 🧹 Remove committed build artifacts and flatten the nested project structure. |

---

**👨‍💻 Built by Ayush Jungari · SudoGrid**
