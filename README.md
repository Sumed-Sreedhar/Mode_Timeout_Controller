# Mode Timeout Controller (STM32)

**Status:** Completed and tested on hardware | STM32F446RE  
**Project Type:** Interrupt- and timer-driven state timeout controller

---

## What It Does
A **mode timeout controller** demonstrating how **time-driven state decay** can be implemented in an interrupt-driven embedded system.

- Button input selects operating modes
- Modes automatically **expire after a fixed time**
- State transitions occur due to both **events** and **time**
- No polling loops, no blocking delays

This project focuses on **state lifetime management**, not pattern complexity.

---

## System Architecture
- **MCU:** STM32F446RE (Nucleo)
- **Input:** Push button (GPIO + EXTI)
- **Output:** LED (GPIO)
- **Timing:** TIM2 periodic interrupt
- **Debug:** ST-Link

---

## Operating States
The system operates in the following modes:

- **OFF** — LED off, idle state  
- **ON** — LED on for a fixed duration  
- **BLINK** — LED blinks for a fixed duration, then exits automatically  

Button presses and timer events both influence state transitions.

---

## System Behavior
- Button presses are handled via **EXTI interrupts**
- EXTI callbacks update **system state only**
- A timer ISR:
  - enforces mode timeouts
  - drives LED behavior
  - performs automatic state decay
- All timing logic is centralized and deterministic

This ensures predictable behavior even without further user input.

---

## Core Concepts Demonstrated
- Time-based state expiration  
- Combining event-driven and time-driven transitions  
- Interrupt-driven mode control  
- Non-blocking firmware design  
- Explicit state lifetime management  

---

## Design Intent
The goal of this project was to:

- Explore **automatic mode timeout** behavior  
- Understand how time can drive state transitions  
- Avoid user-dependent state exits  
- Reinforce clean ISR responsibility separation  

The system was intentionally kept simple to isolate the concept of **state decay over time**.

---

## What I Learned
- How to implement self-expiring states  
- How timers can enforce state lifetime  
- How to combine EXTI and timer logic cleanly  
- Why time-driven transitions are critical in real systems  

---

## Limitations
- Fixed timeout durations  
- Single output  
- No debouncing logic  

These limitations were intentional to keep focus on **time-based behavior**.

---

## Possible Extensions
- Configurable timeout durations  
- Multiple outputs with independent timeouts  
- UART-configurable state lifetimes  
- Integration with higher-level state machines  

---

## Tools & Environment
- STM32CubeIDE  
- STM32 HAL  
- Linux development environment  
- Git & GitHub for version control  

---

## Repository Structure
```
Mode_Timeout_Controller/
├── Core/
│   ├── Src/
│   └── Inc/
├── README.md
└── ...
```

---

## Status
Completed and tested on hardware.
