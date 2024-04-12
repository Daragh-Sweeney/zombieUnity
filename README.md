# ECS7016P Interactive Agents and Procedural Generation Coursework
**Student:** Daragh Sweeney  
**Student ID:** 230732443

**Note:** Very important: make sure the project you open has the following tags: zombie, Supply, Water, Land, Bridge. I noticed that sometimes it would not work when importing into a new project, and this was the reason.

# Scenario
**Zombie Apocalypse**  
- **Environment:** Ocean Islands  
- **Agent A:** Survivor  
- **Agent B:** Zombie

## README Contents
- Introduction
- Setting up environment
- GenerateMap
    - Create Board
    - Connect Landmasses with Bridges
    - Add Water Colliders
- GenerateGame
    - Players (Survivors)
    - Zombies
    - Supplies
    - Astar
- Notes/Future Ideas

## Introduction
As part of the Interactive Agents and Procedural Generation module, we have been tasked with creating a Unity project that implements an agent simulation using behavior trees within a 2D level that is procedurally generated using cellular automata.

As part of the project, we needed to create a map with the following constraints:
- a) Generate an initial 2D grid of filled and empty cells.
- b) Apply cellular automata to the grid.
- c) Post-process the grid to generate the final level.

The agents should also follow:
- There should be at least two types of agents (Agent A and Agent B), controlled (perhaps in part) by behavior trees implemented using the NPBehave library.

## Setting up environment
The Scene created has 4 objects: GenerateMap, GenerateGame, Area Light, and Main Camera.
- GenerateMap uses the CreateBoard script to create the map.
- GenerateGame has the Zombie Spawner, Supply Spawner, and Agent Spawner scripts to spawn the agents.
- Area Light is a light used to get a better view of the map.
- Main camera is used to view the simulation.

## GenerateMap
- **Prefab 1:** Map object is a simple square 2D object.  
**Create Board:**  
    - The board is a 2D array of map objects. As they are created, they are randomly assigned a color and tag (land or water). After this, I run a cellular automata loop. For each tile, I see if it has more than 4 land neighbors. If it does, then it becomes a land tile; if not, then it becomes water. After this process, I also created the coastline by looping through each tile again. If it is land and has 3 or more water tiles bordering it, it becomes yellow.
- **Connect Landmasses with Bridges:**  
    - To connect all landmasses, I first calculated all the tiles that combined to make islands. Then, I picked the largest island and got its closest point to another island. I connected these with a bridge, and now the two islands combined to make a bigger island. I repeated this process until there were no other islands.
- **Add Water Colliders:**  
    - Finally, I added transparent cube objects above the water. I did this as I was having issues with my agents running into the water and breaking the A* pathfinding.

## GenerateGame 
**Prefab 1:** Player - This prefab is a sphere with the yellow material and the Agent Behavior script attached.  
**Prefab 2:** Zombie - This prefab is a sphere with the red material and the Zombie Behavior script attached.  
**Prefab 3:** Supply - This is a cube object with the pink material.  
- **Zombie Spawner script:**  
    - Used to spawn X amount of zombies into the game. The zombie objects use the Zombie Behavior script to dictate their motions. Every 125 ms, they detect how far away the nearest player is and will run fast or slowly towards them depending on how far away they are. They use A* pathfinding to navigate towards the player. If the zombie collides with a player, there is a 50/50 chance they will be destroyed; otherwise, the player will be destroyed. If the player is destroyed, then a new zombie will spawn in their place, although I have noticed this can be buggy at times.
- **Supply Spawner script:**  
    - Used to add supplies to the map. When created, I add a collision handler to each object. If a player collides with the object, then it is destroyed and spawns in a new location on the map.
- **Agent Spawner script:**  
    - Used to spawn X amount of survivors into the game. The player objects use the Player Behavior script to dictate their motions. Every 125 ms, they detect how far away the nearest zombie and supply is. If the zombie is less than 3f away, they will go into a flee mode. If the closest zombie is more than 3f away, they will use A* to move towards the closest supply.
- **Astar script:**  
    - Created a basic version of A* that gets the map from the GenerateMap object. There is a getter in the script. Whoever is using the Astar script will pass in their location and the target location, and a path will be returned.

## Notes/Future Ideas 
Currently, there is no ending. There is a natural ending when either there are no players or no zombies left. If given more time, I would like to have added a restart or banner indicating finishing. Also, I would like to investigate power-ups for the players, a health system, and more dynamic movements for both the player and for the zombie. Creating more interesting and dynamic worlds would also be an interesting topic for future work.
