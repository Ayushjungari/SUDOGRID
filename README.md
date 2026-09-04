# SUDOGRID

> 🧩 Interactive Java-based Sudoku application with a graphical 9×9 puzzle board, move validation, solution viewing, and game controls.

☕ Java · 🖥️ Java Swing · 🎨 AWT · 🛠️ NetBeans

---

## 1. 🎯 Overview

SUDOGRID is an interactive Sudoku application built in Java that allows users to solve a classic 9×9 Sudoku puzzle through a graphical user interface.

Users can select numbers from 1–9, fill empty cells on the board, validate their moves, identify incorrect entries, view the solution when required, and reset or exit the application through interactive controls.

The project demonstrates Java GUI development, event handling, user interaction, and game-state management within a desktop application.

---

## 2. ✨ Features

### 🧩 Interactive Sudoku Board

- Classic 9×9 Sudoku puzzle interface.
- Empty cells can be filled using number selection controls.
- Interactive graphical interface for solving the puzzle.

### 🔢 Number Selection

- Buttons for selecting numbers from 1–9.
- Selected numbers can be entered into available Sudoku cells.
- Provides a simple and interactive way to fill the puzzle.

### ✅ Check Moves

- Validates the moves entered by the user.
- Helps identify correct and incorrect entries.
- Incorrect moves are visually highlighted for easier identification.

### 💡 Solution Controls

- View the complete Sudoku solution using the **Solution** button.
- Hide the displayed solution using the **Hide Solution** option.
- Allows users to continue solving the puzzle independently.

### 🔄 Reset Game

- Reset the Sudoku puzzle and start again.
- Displays a confirmation dialog before resetting the game.

### 🚪 Exit Application

- Exit the application through an interactive control.
- Displays a confirmation dialog before closing the application.

---

## 3. 📜 Sudoku Rules

The objective of Sudoku is to fill the remaining empty cells of a 9×9 grid using numbers from 1–9.

Each number must follow these rules:

- Every row must contain the numbers 1–9 without repetition.
- Every column must contain the numbers 1–9 without repetition.
- Every 3×3 sub-grid must contain the numbers 1–9 without repetition.

---

## 4. 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| Java | Core application logic |
| Java Swing | Graphical user interface development |
| AWT | GUI components and event handling |
| NetBeans | Development environment |

---

## 5. 🔄 Application Workflow

1. Launch the SUDOGRID application.
2. Select a number from the available buttons (1–9).
3. Choose an empty cell on the 9×9 Sudoku board.
4. Enter the selected number into the chosen cell.
5. Use **Check Moves** to validate the entered values.
6. Incorrect entries are highlighted visually.
7. Use **Solution** to view the completed puzzle when required.
8. Use **Hide Solution** to return to the puzzle.
9. Reset the game or exit the application when required.

---

## 6. 📁 Project Features

The application combines multiple interactive components to provide a complete Sudoku-solving experience.

```text
SUDOGRID/
│
├── Sudoku Board
│   └── Interactive 9×9 puzzle grid
│
├── Number Controls
│   └── Number selection from 1–9
│
├── Game Controls
│   ├── Check Moves
│   ├── Solution
│   ├── Hide Solution
│   ├── Reset
│   └── Exit
│
└── Validation
    └── Incorrect move identification
```

---

## 7. 📸 Screenshots

### 🧩 Sudoku Board

<img width="577" height="822" alt="image" src="https://github.com/user-attachments/assets/17aa3421-27eb-43ee-b2d3-295cf8fe8c2f" />

### 💡 Solution View

<img width="580" height="822" alt="image" src="https://github.com/user-attachments/assets/cb6fa15d-758b-489c-827a-3741202d89da" />

### ✅ Move Validation

<img width="573" height="821" alt="image" src="https://github.com/user-attachments/assets/c586a48f-79b4-496a-af59-99c1d46c2c7c" />

### 🔄 Reset and Exit

<img width="576" height="827" alt="image" src="https://github.com/user-attachments/assets/2bdbc4ff-a610-459c-88f4-21b5d0d3af1a" />

---

## 8. ⚙️ Installation & Setup

### 📋 Prerequisites

| Requirement | Details |
|---|---|
| Java | JDK installed on your system |
| NetBeans IDE | Recommended development environment |
| Git | Required to clone the repository |

### 📥 Clone the Repository

```bash
git clone https://github.com/Ayushjungari/SUDOGRID.git
```

### 🚀 Run the Application

1. Open the project in NetBeans IDE.
2. Ensure that Java is properly configured.
3. Build the project.
4. Run the main Java application file.
5. Start solving the Sudoku puzzle.

---

## 9. 🚀 Future Improvements

Potential improvements for the application include:

- Support for multiple Sudoku puzzles.
- Difficulty levels for different users.
- Automatic puzzle generation.
- Timer and score tracking.
- Enhanced user interface and user experience.
- Automatic Sudoku-solving functionality.

---

## 10. 📌 Conclusion

SUDOGRID is a Java-based interactive Sudoku application that provides users with a graphical environment for solving a 9×9 Sudoku puzzle.

The project demonstrates practical concepts of Java GUI development, event handling, user input management, interactive controls, and validation-based functionality.
