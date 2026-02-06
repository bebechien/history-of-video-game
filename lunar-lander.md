# Game Design Document: Lunar Lander

| **Project Name** | Lunar Lander |
| --- | --- |
| **Genre** | Space Flight Simulation |
| **Perspective** | 2D Side-view |
| **Players** | 1 (Single Player) |
| **Platform** | Arcade Cabinet (Vector Display) |
| **Input** | Thrust Lever, 2 Rotation Buttons, Abort Button |

---

## 1. Summary

**Lunar Lander** is a 1979 arcade game developed and published by Atari. It was the first game to utilize Atari's vector graphics engine, providing sharp, high-contrast wireframe visuals. The player assumes the role of a pilot attempting to safely land a lunar module on the Moon's surface. The game is known for its realistic (for the time) physics, requiring careful management of fuel and velocity.

## 2. Gameplay Overview

### 2.1 Core Loop

1. **Descent:** The lander starts at a high altitude with a limited fuel supply.
2. **Navigation:** The player rotates the lander and applies thrust to control both vertical and horizontal velocity.
3. **Landing/Crash:** The lander touches the surface. A successful landing requires low speed and a near-upright angle.
4. **Scoring:** Points are awarded based on the landing quality and the difficulty of the landing site.
5. **Reset:** The game continues with a new terrain layout as long as the player has fuel remaining.

### 2.2 Dynamic Perspective

As the lander approaches the lunar surface, the game automatically zooms in, providing a more detailed view of the landing site. This was a pioneering use of multiple perspectives in arcade gaming.

## 3. Game Mechanics & Controls

### 3.1 Controls

The game features a unique physical interface:
* **Rotate Left / Rotate Right Buttons:** Rotates the module in fixed increments.
* **Thrust Lever:** A large, spring-loaded proportional handle. The intensity of the thrust—and the rate of fuel consumption—is determined by how far the handle is pulled.
* **Abort Button:** A panic button that instantly rotates the lander to a vertical orientation and applies maximum thrust. This consumes a significant amount of fuel but can prevent an imminent crash.

### 3.2 Physics & Resource Management

* **Gravity:** A constant downward force is applied to the lander.
* **Momentum:** The lander possesses inertia; stopping or changing direction requires an opposing force (thrust).
* **Fuel:** Fuel is the primary resource. All actions (rotating, thrusting, aborting) consume fuel. When fuel is exhausted, the lander becomes uncontrollable.
* **Coin-to-Fuel:** Uniquely, players can insert additional coins during play to add more fuel to their current session, allowing for extended gameplay.

## 4. Game Objects (Entities)

### 4.1 The Lunar Module

* **Visual:** A wireframe representation of the Apollo Lunar Module.
* **Components:** Engine (bottom), rotation jets (sides).

### 4.2 The Moon Surface

* **Terrain:** A single screen-width of jagged, scrolling terrain that wraps endlessly.
* **Landing Pads:** Specific flat sections of the terrain marked with flashing multipliers (e.g., 2x, 5x, 10x).

## 5. Scoring & Progression

### 5.1 Landing Quality

Points are awarded based on the vertical and horizontal speed at the moment of impact. A "Good" or "Excellent" landing provides significantly more points and a small fuel bonus.

### 5.2 Multipliers

Landing on narrower, more difficult-to-reach pads multiplies the base landing score.
* **Wide Pads:** 2x multiplier.
* **Medium Pads:** 5x multiplier.
* **Narrow Pads:** 10x multiplier.

### 5.3 Difficulty Levels

The player can select from four difficulty levels (Training, Standard, Pro, and Astronaut), which affect fuel consumption, gravity, and control responsiveness. In "Astronaut" mode, the lander continues to rotate even after the button is released, requiring counter-rotation to stabilize.

## 6. Audio & Visuals

### 6.1 Visual Style

* **Vector Graphics:** Sharp, monochromatic white lines on a black background.
* **HUD:** Displays altitude, vertical/horizontal speed, score, and remaining fuel at the top of the screen.

### 6.2 Sound Effects

* **Thrust:** A modulated "roar" that changes in intensity with the lever position.
* **Alerts:** Beeping sounds to warn of low fuel or high descent speeds.
* **Crash:** A loud explosion sound created by white noise.

## 7. Technical Specifications

* **CPU:** MOS Technology 6502 (running at ~1.5 MHz).
* **Display:** Monochrome X-Y Vector Monitor.
* **Hardware:** Atari 6502 Vector engine.
