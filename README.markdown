# Assignement - 2

## Table of Contents
- [Project 1: Traffic Light System](#project-1-traffic-light-system)
- [Project 2: Reaction Time Game](#project-2-reaction-time-game)

## Project 1: Traffic Light System

### Features
- **Standard Traffic Light Sequence**:
  - **Red**: 20 seconds (stop).
  - **Red + Yellow**: 5 seconds (prepare to go).
  - **Green**: 10 seconds (go).
  - Runs in an infinite loop.
- **Pedestrian Button Integration**:
  - During **Green**: Button press triggers immediate transition to **Green + Yellow** (5 seconds), then **Red**.
  - During **Red**: Button press extends the **Red** phase by 10 seconds.

### Pin Configuration
| Component | Pin | GPIO Port |
|-----------|-----|-----------|
| R_LED     | PA5 | GPIO_OUT  |
| Y_LED     | PA6 | GPIO_OUT  |
| G_LED     | PA7 | GPIO_OUT  |
| EXT_BTN   | PA4 | GPIO_IN   |

### Circuit Diagram
```
                    STM32F767
                  ┌─────────────┐
                  │             │
    R_LED     ────┤ PA5         │
                  │             │
    Y_LED     ────┤ PA6         │
                  │             │
    G_LED     ────┤ PA7         │
                  │             │
    EXT_BTN   ────┤ PA4         │
                  │             │
                  │         GND ├──── GND
                  │         3V3 ├──── 3.3V
                  └─────────────┘
```

### Demo Video
*(Link to demo video will be added here)*

## Project 2: Reaction Time Game

### Features
- **Random Timing**: Reflex LED (LD3) activates randomly within 3–20 seconds.
- **False Start Detection**: Pressing before LD3 activation awards victory to the opponent.
- **Winner Indication**: Winner's LED remains on until system reset.
- **Fair Competition**: Edge detection ensures the first press wins.
- **Hardware Reset**: Use the STM32 reset button to restart the game.

### Game Rules
- Game starts automatically after reset.
- LD3 turns on randomly within 20 seconds.
- First player to press their button after LD3 activation wins.
- Pressing before LD3 (false start) awards the win to the opponent.
- Winner's LED stays on until the system is reset.

### Pin Configuration
| Component | Pin | GPIO Port |
|-----------|-----|-----------|
| R_LED     | PA5 | GPIO_OUT  |
| P1_LED    | PA6 | GPIO_OUT  |
| P2_LED    | PA7 | GPIO_OUT  |
| P1_BTN    | PA4 | GPIO_IN   |
| P2_BTN    | PB4 | GPIO_IN   |

### Circuit Diagram
```
                    STM32F767
                  ┌─────────────┐
                  │             │
    R_LED     ────┤ PA5         │  Reflex LED
                  │             │
    P1_LED    ────┤ PA6         │  Player 1 Win LED
                  │             │
    P2_LED    ────┤ PA7         │  Player 2 Win LED
                  │             │
    P1_BTN    ────┤ PA4         │  Player 1 Button
                  │             │
    P2_BTN    ────┤ PB4         │  Player 2 Button
                  │             │
                  │         GND ├──── GND
                  │         3V3 ├──── 3.3V
                  └─────────────┘
```

### Demo Video
[![Reaction Game Demo](https://img.youtube.com/vi/uce8lnO9HEw/0.jpg)](https://www.youtube.com/watch?v=uce8lnO9HEw)

