# dodge-the-creeps-game
Repository used to host my modified dodge the creeps game.

## Overview
This is a modified version of the "Dodge the Creeps" game from the Godot Engine 2D tutorial. The game includes several enhancements to increase difficulty and improve gameplay mechanics.

## Game Modifications
### Visual and Gameplay Balance Changes

-Player and mob sprite scaling: Reduced sprite sizes to create a more challenging visual experience, making precision movement more critical for survival
-Enhanced mob path configuration: Modified the mob spawn path to increase enemy density within the game screen, ensuring players encounter more frequent threats and requiring constant vigilance
-Balanced mob spawn frequency: Reduced the mob timer frequency to compensate for increased enemy speed and density, preventing the game from becoming impossibly difficult while maintaining an engaging challenge level

### Three-Life System Implementation
-The most significant modification was implementing a comprehensive three-life system with visual feedback through heart icons.

### Heart UI System

-Added three heart TextureRect nodes to the HUD scene positioned in the top-left corner
-Integrated heart images to provide clear visual representation of remaining lives
-Implemented dynamic heart visibility system where hearts disappear as lives are lost

## Core Life Management Logic
The life system required extensive modifications to the main game logic:
Main.gd modifications:

Added a lives variable initialized to 3 at game start
Modified the _on_player_hit() function to decrement lives instead of immediately triggering game over
Implemented conditional game over logic that only ends the game when all three lives are exhausted
Added player respawn functionality that repositions the player at the starting location after each hit

## HUD.gd enhancements:

-Created update_lives() function to manage heart visibility based on remaining lives
-Integrated life counter with the existing score and message display systems

-Technical Challenges and Solutions
Several significant technical hurdles were encountered during implementation:
Collision Detection Issues: After the first collision, the player would lose collision detection capability, preventing subsequent hits from registering. This required careful management of the Area2D node's monitoring properties and CollisionShape2D enabling/disabling states. For this i was not able to figure it out using youtube videos took direct help from AI.
Signal Connection Problems: Initially, player hit signals were incorrectly connected to the player script instead of the main scene script, causing the life management logic to fail. This required proper signal routing from Player.hit to Main._on_player_hit().
Game State Management: The game would incorrectly display start UI elements during mid-game respawns. This necessitated careful separation of game restart logic from player respawn logic.
Player Respawn Mechanics: Ensuring the player could be hit multiple times required precise timing of collision shape re-enabling and proper reset of the player's Area2D monitoring capabilities.
The final implementation successfully provides players with three lives, complete with visual feedback, while maintaining the game's core mechanics and challenge level. The only bug i couldnt fix or rather logic was how to get the timer to continue till the end, i always got some logic error with it so i finally just made it in essence restart the game without the HUD elemented whenever we lose a life and I allow it to do that three times before it says game over. I just made it work, there should be a better way to do this for sure.
