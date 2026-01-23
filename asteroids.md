# Game Design Document: Asteroids

| **Project Name** | Asteroids |
| --- | --- |
| **Genre** | Multi-directional Shooter |
| **Perspective** | 2D Top-down (Wraparound Screen) |
| **Players** | 1 (Single Player) |
| **Platform** | Arcade Cabinet (CRT Monitor) |
| **Input** | 5 Buttons |

## 1. Summary

**Asteroids** is a single-player, multi-directional shooter where the player pilots a spaceship trapped in a deadly asteroid field. The objective is survival: destroy asteroids and hostile flying saucers to accumulate points. The game utilizes a vector display to create sharp, high-contrast wireframe graphics. The key differentiator is the implementation of Newtonian physics (inertia), requiring players to carefully manage momentum rather than just position.

## 2. Gameplay Overview

### 2.1 Core Loop

1. **Spawn:** Player ship appears in the center of the screen.
2. **Survive:** Avoid collision with drifting asteroids and enemy saucers.
3. **Destroy:** Shoot asteroids to break them into smaller pieces; shoot saucers for bonus points.
4. **Progress:** When all asteroids are cleared, a new, more difficult wave begins.

### 2.2 Screen Mechanics

* **Toroidal Topology (Screen Wrap):** The game world is a single screen with "wrap-around" physics. An object exiting the right side immediately re-enters on the left; exiting the top re-enters at the bottom. This applies to the player, enemies, and projectiles.

## 3. Game Mechanics & Controls

### 3.1 Controls

The arcade cabinet utilizes a five-button control scheme (no joystick).

* **Rotate Left:** Rotates the ship counter-clockwise.
* **Rotate Right:** Rotates the ship clockwise.
* **Thrust:** Applies force in the direction the ship is facing.
* **Fire:** Launches a projectile.
* **Hyperspace:** Instantly teleports the ship to a random screen location (high risk).

### 3.2 Physics Engine

* **Inertia:** The ship does not stop moving when the "Thrust" button is released. It drifts in the last vector of acceleration. To stop, the player must rotate 180 degrees and thrust against their current momentum.
* **Friction:** There is effectively zero friction in the vacuum of space.

### 3.3 Hyperspace Mechanics

When activated, the ship vanishes and reappears at a random coordinate.

* **Risk:** There is a probability that the ship will respawn directly inside an asteroid or appear just as a saucer fires, resulting in immediate death.
* **Usage:** Intended as a "panic button" of last resort.

## 4. Game Objects (Entities)

### 4.1 The Player Ship

* **Visual:** A simple isosceles triangle.
* **Capabilities:** Can rotate 360 degrees, fire up to 4 bullets at a time on screen.

### 4.2 The Asteroids

Asteroids are the primary environmental hazard. They drift at varying angles and speeds.

* **Lifecycle:**
1. **Large Asteroid:** Slow moving. When shot, breaks into **2 Medium Asteroids**.
2. **Medium Asteroid:** Medium speed. When shot, breaks into **2 Small Asteroids**.
3. **Small Asteroid:** Fast moving. When shot, it is destroyed completely.

### 4.3 Flying Saucers (UFOs)

Periodic enemies that appear from the edges of the screen to disrupt the player.

* **Large Saucer:**
* **Behavior:** Moves horizontally/diagonally across the screen. Fires randomly.
* **Purpose:** To force the player to move if they are camping.

* **Small Saucer:**
* **Behavior:** Appears later in the game (higher score thresholds). Moves across the screen.
* **AI:** Aim is highly accurate. It calculates the player's trajectory and fires to intercept.

## 5. Scoring & Progression

### 5.1 Point Values

| Entity | Description | Points |
| --- | --- | --- |
| **Large Asteroid** | Slow, easy target. | 20 |
| **Medium Asteroid** | Faster. | 50 |
| **Small Asteroid** | Very fast, hard to hit. | 100 |
| **Large Saucer** | Random shots. | 200 |
| **Small Saucer** | Precision shots. | 1,000 |

### 5.2 Difficulty Progression

* **Wave Difficulty:** Each subsequent wave spawns with more Large Asteroids (starting with 4, increasing up to a cap).
* **Saucer Frequency:** Saucers appear more frequently as the game progresses.
* **Extra Life:** Awarded every 10,000 points.

## 6. Audio & Visuals

### 6.1 Visual Style

* **Vector Graphics:** High-intensity white lines on a black background.
* **Brightness:** Shots and explosions should be brighter (higher intensity) than static rocks.

### 6.2 Sound Effects

* **Heartbeat:** A background pulse tone that increases in tempo as the number of asteroids on screen decreases, inducing tension.
* **Thrust:** A continuous white noise hiss.
* **Fire:** A high-pitched "pew".
* **Explosion:** A rough, crumbling noise.
* **Saucer:** A distinct warbling siren to alert the player of an enemy presence even if off-screen.

## 7. Technical Specifications

* **Display:** Vector Monitor (Quadrascan).
* **CPU:** MOS Technology 6502 (1.5 MHz).
* **Resolution:** 1024 x 768 (effective vector resolution).
* **Frame Rate:** Variable (dependent on the number of vectors drawn on screen).
