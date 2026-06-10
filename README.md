# 🎮 Tic-Tac-Toe — Midnight Neon Edition

A professional-grade, fully object-oriented Tic-Tac-Toe game built with **Java Swing**, featuring a custom dark-mode "Midnight Neon" UI theme, live score tracking, and clean OOP architecture.

---

## ✨ Features

| Feature | Details |
|---|---|
| 🎨 Dark Mode UI | Custom "Midnight Neon" palette — deep navy background, cyan X, amber O |
| 📊 Score Tracker | Persistent win counters for both players across multiple rounds |
| 🔄 Reset Button | Start a new game at any time without closing the app |
| 💡 Turn Indicator | Glowing dot highlights the active player in the score panel |
| 🏆 Win Detection | Checks all 8 winning lines (3 rows, 3 cols, 2 diagonals) |
| ✋ Draw Detection | Announces a stalemate when the board fills with no winner |
| 🖱️ Hover Effects | Cells brighten on mouse hover for tactile feedback |

---

## 🏗️ Architecture

The project follows clean OOP separation of concerns across three classes:

```
src/
├── Main.java       # Entry point — launches the EDT and creates GameUI
├── GameLogic.java  # Pure game engine: board state, rules, win/draw logic
└── GameUI.java     # All Swing components, event handling, visual feedback
```

### Class Responsibilities

**`GameLogic`** — knows nothing about Swing.  
Manages the 9-cell board array, validates moves, checks win conditions against all 8 possible lines, detects draws, and tracks cumulative scores. Can be unit-tested independently.

**`GameUI`** — knows nothing about game rules.  
Builds the JFrame hierarchy (title bar → score panel + grid → status bar), handles button clicks, delegates to `GameLogic`, and reflects results back through labels, colors, and repaints.

**`Main`** — five lines.  
Schedules `GameUI` creation on the Swing Event Dispatch Thread using `SwingUtilities.invokeLater()`.

---

## 🔍 Win Detection Logic (explained)

The board is stored as a flat `char[9]` array indexed like this:

```
0 | 1 | 2
---------
3 | 4 | 5
---------
6 | 7 | 8
```

All 8 winning lines are pre-declared as index triplets:

```java
private static final int[][] WIN_COMBINATIONS = {
    {0,1,2}, {3,4,5}, {6,7,8},   // rows
    {0,3,6}, {1,4,7}, {2,5,8},   // columns
    {0,4,8}, {2,4,6}             // diagonals
};
```

After every move, `checkWin()` iterates over all 8 and returns `true` the moment it finds a triplet where all three cells are equal **and** non-empty.

---

## 🚀 How to Run in VS Code

### Prerequisites
- Java Development Kit (JDK) 11 or higher
- VS Code with the **Extension Pack for Java** installed

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/tic-tac-toe-java.git
   cd tic-tac-toe-java
   ```

2. **Open in VS Code**
   ```bash
   code .
   ```

3. **Run from the terminal**
   ```bash
   # Compile all three source files
   javac src/*.java -d out

   # Run the Main class
   java -cp out Main
   ```

   Or simply open `Main.java` in VS Code and click the **▷ Run** button that appears above the `main` method.

### Running without VS Code (plain terminal)
```bash
mkdir -p out
javac src/GameLogic.java src/GameUI.java src/Main.java -d out
java -cp out Main
```

---

## 📸 UI Overview

```
┌─────────────────────────────────────┐
│         TIC-TAC-TOE                 │
├──────────────┬──────────────────────┤
│  ● PLAYER X  │  ┌───┬───┬───┐      │
│    X  3      │  │ X │   │ O │      │
│              │  ├───┼───┼───┤      │
│  ○ PLAYER O  │  │   │ X │   │      │
│    O  2      │  ├───┼───┼───┤      │
│              │  │ O │   │ X │      │
│              │  └───┴───┴───┘      │
├──────────────┴──────────────────────┤
│        Player X wins! 🎉            │
│            [ NEW GAME ]             │
└─────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

- **Language:** Java 11+
- **GUI Framework:** Java Swing (javax.swing)
- **Build:** Plain `javac` — no Maven/Gradle required
- **Lines of code:** ~350

---

## 📄 License

MIT — free to use, modify, and showcase in your own portfolio.
