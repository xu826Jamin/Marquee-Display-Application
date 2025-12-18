# Marquee-Display-Application
## Overview
This project implements a **Marquee Display** application in C. It simulates a scrolling text display in the terminal, similar to those seen on stock tickers or news banners. The program solves the problem of displaying a dynamic message within a fixed-width window by continuously scrolling the text. It demonstrates the fundamental "Game Loop" architecture used in real-time applications and games.

## Features
- **Dynamic Marquee Scrolling:** Continuously scrolls a text message horizontally within a 20-character window.
- **Interactive Input:** Users can type alphanumeric characters (A-Z, a-z, 0-9) in real-time to append them to the scrolling message.
- **Direction Control:** Pressing the **Space Bar** toggles the scrolling direction between left and right.
- **Exit Command:** Pressing **'#'** safely terminates the program.
- **Constraints & Edge Cases:**
  - Handles string wrapping using modulo arithmetic to create a seamless loop.
  - Limits the message length to 40 characters (including `>>` header and `<<` footer) to prevent buffer overflows.
  - Ignores invalid input characters to maintain display integrity.

## Tech Stack
- **Language:** C
- **Build System:** GNU Make
- **Libraries:** 
  - `MacUILib` (Custom library for cross-platform terminal UI and input handling)
  - Standard C Library (`stdio.h`)

## Design Decisions
**Asynchronous Input Handling:**
One key design decision was to use **asynchronous (non-blocking) input**. 
- **Tradeoff:** This makes the input handling logic slightly more complex than simple `scanf` or `getchar` calls because we must check `MacUILib_hasChar()` in every loop iteration.
- **Why:** This is crucial for the application because the marquee animation needs to keep updating and drawing frames even when the user is not typing. A blocking input call would freeze the animation until a key was pressed.

## How to Run
1. **Compile the project:**
   Open a terminal in the project directory and run:
   ```bash
   make
   ```
2. **Run the executable:**
   - On Windows:
     ```bash
     .\PPA1.exe
     ```
   - On Linux/Mac:
     ```bash
     ./PPA1
     ```
3. **Clean up:**
   To remove compiled files:
   ```bash
   make clean
   ```

## What I Learned
- **Game Loop Architecture:** Gained practical experience implementing the standard `Initialize` -> `Input` -> `Logic` -> `Draw` -> `Delay` -> `Cleanup` loop structure.
- **State Management:** Learned to manage application state (like scroll index and direction) across different phases of the loop.
- **Circular Buffering:** Applied modulo arithmetic (`%`) to implement the wrapping logic for the scrolling text.
- **Terminal Manipulation:** Understood how to clear and redraw the screen frame-by-frame to create the illusion of animation.
