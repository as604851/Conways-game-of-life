
# Conway's Game of Life Simulation

## Overview
This project implements a simple simulation of **Conway's Game of Life** using **C++**. Conway's Game of Life is a cellular automaton where cells on a grid evolve over time based on a set of predefined rules. The program initializes a **9x9** board with predefined live (`'o'`) and dead (`' '` or empty) cells and continuously updates the board according to the Game of Life rules.

The simulation runs in an infinite loop, updating the board state and displaying it in real time, showcasing fundamental C++ techniques such as board manipulation, game logic, and console output handling.

## Features
- **Board Initialization**:
  - The grid starts with a predefined configuration of live (`'o'`) and dead cells.
  - The initial setup provides a starting point for the simulation to evolve dynamically.
  
- **Game Logic (Conway’s Rules)**:
  - Each cell's state is updated based on its neighboring cells:
    - **Survival**: A live cell (`'o'`) with 2 or 3 neighbors remains alive.
    - **Overpopulation**: A live cell with more than 3 neighbors dies.
    - **Underpopulation**: A live cell with fewer than 2 neighbors dies.
    - **Reproduction**: A dead cell with exactly 3 neighbors becomes alive.
  
- **Real-time Board Display**:
  - The board state is cleared and updated in each iteration using `system("CLS")` to refresh the screen.
  - The board is displayed using the `printBoard()` function.
  
- **Continuous Game Loop**:
  - The simulation runs indefinitely, updating the board state at each step until manually terminated by the user.

## Installation & Usage

### Prerequisites
- **Operating System**: Windows (due to dependencies like `conio.h` and `windows.h`).
- **C++ Compiler**: A C++ compiler supporting C++11 or later (such as **MinGW/g++** or **MSVC**).

### Steps to Compile and Run
1. **Clone the Repository**:
   ```sh
   git clone https://github.com/your-username/game-of-life-simulation.git
   cd game-of-life-simulation
   ```

2. **Compile the Program**:
   ```sh
   g++ -o game_of_life game_of_life.cpp -std=c++11
   ```

3. **Run the Executable**:
   ```sh
   ./game_of_life
   ```

## Code Explanation

### 1. Board Initialization
The program initializes two **9x9** arrays (`f` and `g`) representing the board at different stages:

```cpp
char f[9][9] = {
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', 'o', ' ', ' ', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '},
    {' ', ' ', 'o', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', 'o', ' ', ' ', 'o', ' ', ' '},
    {' ', ' ', ' ', ' ', ' ', ' ', ' ', ' ', ' '}
};
```

`f` represents the initial board configuration, while `g` is used for storing the next state.

### 2. Print Board Function
The `printBoard()` function is used to display the board state:

```cpp
void printBoard(char board[9][9]) {
    for (int i = 0; i < 9; i++) {
        for (int j = 0; j < 9; j++) {
            std::cout << board[i][j] << " ";
        }
        std::cout << std::endl;
    }
}
```

### 3. Game Loop and Logic
The main loop continuously updates the board:

```cpp
int main() {
    int b = 0, a = 0;
    char f[9][9], g[9][9];  
start:
    for (int y = 0; y < 9; y++) {
        for (int x = 0; x < 9; x++) {
            g[y][x] = ' ';
        }
    }

    for (int y = 0; y < 9; y++) {
        for (int x = 0; x < 9; x++) {
            if (f[y][x] == 'o') { a++; }
            if (f[y][x + 1] == 'o') { b++; }
            if (f[y][x - 1] == 'o') { b++; }
            if (f[y + 1][x] == 'o') { b++; }
            if (f[y - 1][x] == 'o') { b++; }
            if (f[y + 1][x + 1] == 'o') { b++; }
            if (f[y + 1][x - 1] == 'o') { b++; }
            if (f[y - 1][x + 1] == 'o') { b++; }
            if (f[y - 1][x - 1] == 'o') { b++; }

            if (b < 2 || b > 3) { g[y][x] = ' '; }
            else if (b == 3 || (b == 2 && f[y][x] == 'o')) { g[y][x] = 'o'; }

            b = 0; a = 0;
        }
    }

    Sleep(100);
    system("CLS");
    printBoard(g);
    
    for (int y = 0; y < 9; y++) {
        for (int x = 0; x < 9; x++) {
            f[y][x] = g[y][x];
        }
    }

    goto start;
    return 0;
}
```

### 4. Continuous Updates
- The board is cleared and refreshed at each step.
- The updated state is displayed using `printBoard()`.
- The loop runs indefinitely, simulating the evolution of the board.

---
This project provides a fundamental implementation of Conway's Game of Life and can be expanded with user input, a graphical interface, or different board sizes.
