# 🍔 Kitchen Rush

**Kitchen Rush** is an interactive, browser-based cooking game developed using JavaScript, HTML5 Canvas, and Node.js. Players take on the role of a chef tasked with collecting ingredients from a moving conveyor belt and assembling recipes at the correct cooking stations.

The game combines real-time movement, randomized ingredient generation, sequential recipe validation, and progressively increasing difficulty to create an engaging cooking challenge.

## 🛠️ Technologies Used

**Frontend**
- JavaScript
- HTML5 Canvas API

**Backend**
- Node.js
- Express.js

**Development Environment & Version Control**
- Ubuntu Linux
- Oracle VirtualBox
- Visual Studio Code Remote - SSH
- Git and GitHub

The game was developed in an Ubuntu Linux virtual machine using Oracle VirtualBox, with VS Code Remote - SSH providing access to the development environment.

## 🎮 How to Play

### Objective

Complete randomly selected recipes by collecting the correct ingredients from the conveyor belt and placing them at the corresponding cooking station.

The game features **3 recipes**:

| Recipe | Required Ingredients (in order) |
|---|---|
| 🍔 Burger | Bottom Bun → Beef → Cheese → Top Bun |
| 🍦 Ice Cream | Cone → Ice Cream |
| 🧇 Waffle | Waffle → Chicken → Syrup |

### Controls

| Key | Action |
|---|---|
| Enter / Return | Start or restart the game |
| ← Left Arrow | Move the chef left |
| → Right Arrow | Move the chef right |
| Spacebar | Collect and place an ingredient |

### Game Rules

1. Press **Enter** to begin the game.
2. A random recipe appears at the top-left corner of the screen.
3. Move the chef left or right to collect ingredients from the conveyor belt.
4. Position the chef near the required ingredient and press **Spacebar**.
5. Make sure you are at the correct cooking station and collect ingredients in the exact recipe order.
6. Successfully completing a recipe increases your score by **1 point** and generates a new recipe.
7. Selecting the wrong ingredient or placing an ingredient at the wrong station ends the game.
8. Press **Enter** or use the restart button to play again.

### Difficulty Progression

The game becomes more challenging as the player earns points.

- **0–2 points:** Conveyor speed is set to 3 units per update.
- **3+ points:** Conveyor speed increases to 5 units per update, a **66.7% increase**.
- A congratulatory message appears every 3 completed recipes.

## 🚀 How to Run the Game Locally

### Prerequisites

Ensure you have the following installed:

- Node.js
- npm
- Git

### Installation

```bash
git clone https://github.com/Nabiha072005/kitchen-rush.git
```bash
cd kitchen-rush
```bash
npm install
```bash
node server.js
```bash
Visit:
```bash
`http://localhost:3001`
```bash

The Express server serves the game's HTML, JavaScript, and image assets from the `public` directory.

*Note: If the server is running inside a virtual machine or remote environment, port forwarding may be required to access the game from your host computer.*

## 💻 Technical Implementation

### 1. Object-Oriented Game Architecture

Implemented reusable JavaScript constructor functions to represent interactive game entities.

- **Chef:** Manages player position, movement speed, and rendering.
- **ConveyorIngredient:** Manages ingredient properties, movement, and rendering.

Constructor-based object-oriented programming allows multiple ingredient objects to share a consistent structure and behavior without requiring separate movement logic for each ingredient type.

### 2. Real-Time Game Loop

Implemented a continuous game loop using JavaScript's `setInterval()` function, configured to execute every **20 milliseconds**, targeting **50 updates per second**.

The update loop handles:

- Player movement and keyboard input
- Conveyor belt animation
- Ingredient spawning and movement
- Game-state updates
- Rendering of game objects and interface elements

### 3. Probability-Based Ingredient Generation

Designed a randomized ingredient spawning algorithm using `Math.random()`.

- Supports **9 unique ingredient types** across 3 recipes.
- Assigns a **33.3% probability** to spawning the currently required ingredient.
- Uses the remaining probability to select a random incorrect ingredient.
- Generates ingredients every **90 game updates**, targeting approximately **1.8-second intervals**.

This introduces unpredictability and requires players to react to changing conveyor-belt contents.

### 4. Proximity-Based Ingredient Selection

Implemented distance-based selection logic to identify ingredients within the chef's collection range.

The algorithm calculates the horizontal distance between the chef and nearby ingredients, selecting the closest eligible ingredient within a **50-pixel threshold**.

### 5. Sequential Recipe Validation

Implemented ordered recipe validation using arrays and a recipe index.

Each collected ingredient is checked against:

- The next required ingredient in the recipe.
- The cooking station corresponding to the selected recipe.

Correct selections advance recipe progress, while incorrect selections trigger the game-over state.

### 6. Dynamic Difficulty Scaling

Implemented score-based difficulty progression that automatically increases conveyor speed from **3 to 5 units per update** once the player reaches 3 points.

This represents a **66.7% increase in conveyor speed**, creating a progressively more demanding gameplay experience.

### 7. Game-State Management

Developed game-state logic to manage:

- Start screen
- Active gameplay
- Score tracking
- Recipe progression
- Game-over conditions
- Restart functionality

