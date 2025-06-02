# ASCII Snake Game in C

This is a simple **Snake game implemented in C**, playable directly from your terminal. It uses basic C structures, ANSI escape codes for colors, and grid logic to simulate a real-time game loop — all without any external libraries.

---

##  How to Play

Use the **WASD keys** to move the snake:

- `W` – up  
- `A` – left  
- `S` – down  
- `D` – right

Eat the apples (`0`) to grow the snake (`1`) and increase your score.

If you crash into yourself, the game ends.

---

##  Compilation

```bash
gcc snake.c -o snake
./snake
```


## Features & Concepts
**Snake Representation (Linked List)**
- The snake is implemented as a singly linked list (struct snake) where each node stores an (x, y) position.
- The head is the active part of the snake that moves, and when the snake eats an apple, a new head is added at the front.
- Movement is implemented recursively: each node moves to the position of the node in front of it.

**Apple Generation & Eating**
- The apple is defined as a simple struct with (x, y) coordinates.
- It is randomly placed on the grid using rand() and regenerated only in an empty cell.
- When the snake head reaches the apple's coordinates:
  - The snake grows by adding a new head node.
  - A new apple is generated.
  - Score increases by 10.

**Grid Drawing & ASCII Graphics**
- The game uses a 2D character array grid[ROW][COL] to represent the playing field.
- ' ' represents an empty cell, '1' is a snake body part, and '0' is the apple.
- Each frame:
  - The grid is cleared
  - Snake and apple are drawn
  - The full grid is printed with borders and colors

**Colored Output (ANSI Escape Codes)**
- Snake body is printed in green
- Apple is printed in red
- Score text is also highlighted using ANSI codes like \033[0;32m, \033[0;31m, and reset with \033[0m

**Repainting Without Scrolling**
- The code uses \x1b[H to move the cursor to the top-left of the terminal.
- This avoids printing new lines and simulates real-time frame updates without terminal clutter.

**Movement Wrapping (Toroidal Logic)**
- If the snake moves off the screen, it wraps around to the other side:
  - `(x - 1 + COL) % COL` keeps the position inside the grid
- This creates a toroidal field (like Pac-Man)

**Collision Detection**
- The game checks if the snake is about to move into itself using check_collision()
- If a collision is detected, the game ends and displays the final score

**Clean Exit on Game Over**
- When the snake collides with itself:
  - The game clears the screen
  - Prints "GAME OVER FINAL SCORE: X" in red
  - Exits using exit(0)

**Input Handling**
- Movement is handled using getchar()
- Input is blocking and requires pressing Enter after each move
- Can be improved using termios.h or ncurses for real-time key capture

**Score System**
- Score starts at 0
- Increases by 10 points per apple
- Displayed at the top of the screen in red
