                                                                                                                                                                    
 # Oregon Trail Adventure Decision Game (Lite)

**Author:** Tyler Osso  
**Date:** May 9, 2025  
**Revision:** 1.0

---

## Overview

This is a "lite" LC-3 Assembly version of the classic Oregon Trail decision game.  
Players are prompted with a series of scenarios and must choose one of four options. Each choice carries a different penalty to your party’s size or miles remaining. There is **no win condition**—the game ends when you run out of party members or miles or you proceed past question 4

---

## Features

- 4 Prompted decision points (Questions 1–4)  
- Party‐size and miles‐remaining tracking  
- Random events via a custom TRAP routine (x38)  
- Input sanitization for menu choices  
- Game‐over screen showing final status  

---

## Requirements

- LC-3 Assembly simulator (e.g. PennSim, LC3Edit) -- Mac OS LC3Tools Version 2.0.2 (2.0.2) by Chirag Sakhuja used to make this --
- A single `.asm` source file containing the main program

---

## Assembling & Running

1. **Assemble** the .asm source file (e.g. `oregon_trail.asm`):
2. **Set Stop Points At Halts**  `x300D`  `x333F` and  `x382B`
3. **Run** starting at `x3000`.  
   The game will:
   1. Clear and initialize registers and data (JSR INITIALIZE_GAME).  
   2. Greet you and read your name (JSR WELCOME_LOOP).  
   3. Step through three decision questions (JSR QUESTION_ONE, TWO, THREE), each followed by a status update (JSR STATUS_OF_PARTY).  
   4. Call TRAP x38 for a random event, then update the party (JSR UPDATE_PARTY).  
   5. Present a final update question.
   6. Go to game over screen with update
4. **Play Again** Just set start point back at `x3000`
---

## Code Structure

| Section / Subroutine    | Purpose                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------|
| **INITIALIZE_GAME**     | Clears all registers, sets up stack pointer, party size, miles remaining, and trap vector |
| **WELCOME_LOOP**        | Prints welcome message, reads and stores player name                                     |
| **QUESTION_ONE**        | Presents river‐crossing scenario and applies penalties                                   |
| **QUESTION_TWO**        | Presents fever scenario and applies penalties                                            |
| **QUESTION_THREE**      | Presents mountain‐pass scenario and applies penalties                                    |
| **UPDATE_PARTY**        | Adds TRAP‐returned random number (R1) 0-9 to party size                                      |
| **STATUS_OF_PARTY**     | Displays current party size and miles remaining                                          |
| **CHECK_ANSWER**        | Validates input (1–4), reprompts on bad input                                            |
| **GAME_OVER**           | Prints “Game Over” banner, calls STATUS_OF_PARTY, then HALTs                              |
| **PRINT_USER_NAME**     | Helper to echo stored player name                                                        |
| **Custom TRAP x38**     | Polls KBSR/KBDR to generate a pseudo-random 0–9 value and prints “X members joined…”      |
| **Question_Four**       | Presents final question that triggers game over scenario                                   |


![image](https://github.com/user-attachments/assets/ec34b201-8baf-4bbc-b5d7-e81d5e17434a)

![image](https://github.com/user-attachments/assets/b211349f-4493-487a-bac1-2bea37c6671a)

![image](https://github.com/user-attachments/assets/5493d8b1-df7b-4753-9990-eb9eb6681fff)

