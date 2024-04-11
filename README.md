# ECS7016P Interactive Agents and Procedural Generation Coursework
Stundent: Daragh Sweeney 
Student ID: 230732443

# Scenario
**Zombie Apocalypse**
- **Environment:** Ocean Islands
- **Agent A:** Survivor
- **Agent B:** Zombie

## README Contents
- Introduction
- Setting up environment
- GenerateMap
    - create board
    - Connect Landmasses with Bridges
    - Add Water Colliders
- GenerateGame
    - Players (Survivors)
    - Zombies
    - Supplies


## Introduction
As part of the Interactive Agents and Procedural Generation module we have been tasked with creating a Unity project 
that implements an agent simulation using behaviour trees within a 2D level that is procedurally generated using cellular automata.

As part of the project we needed to create a map with the following restraints 
- a) Generate an initial 2D grid of filled and empty cells.
- b) Apply cellular automata to the grid.
- c) Post-process the grid to generate the final level

The agents should also follow 
- There should be at least two types of agent (Agent A and Agent B), controlled (perhaps in-part) by behaviour trees implemented using the NPBehave library.

## Setting up environment
The Scene created has 4 objects, GenerateMap, GenerateGame, Area  Light and Main Camera

- GenerateMap uses the create board scrip, to create the map
- GenerateGame has the Zombie Spawner, Supply Spwner and Agent Spawner scrips to spawn the agents
- Area Light is a light I used to get a better view of the map
- Main camera is used to view the simulation

## GenerateMap

prefab1 - map object is a simple square 2d object 
create board script is used to create the map 

- create board: the board is a 2d array of mapObjects, as they are created they are randomly assigned a color and tag, land or water. After this I run a cellular automata loop, for each tile i see if it has more than 4 land neighbours, if it does then it becomes a land tile, if not then it becomes water, after this process I also created the coastline by looping through each tile again and if it is land and has 3 or more water tiles boardering it becomes yellow.
- Connect Landmasses with Bridges: To connect all landmasses i first calculated all the tiles that combined to make islands, I then picked the largest island and got its closest point to another island, I connected these with and bridge and now the two islands combined to make a bigger island, i repeated until there were no other islands 
- Add Water Colliders: finally I added transparent cube objects above the water, I did this as I was having issues with my agents running into the water and breaking the astar pathfindin



## GenerateGame 
prefab1 - player, this prefab is a sphere with the yellow material and the Agent Behaviour script attached
prefab2 - Zombie, this prefab is a sphere with the red material and the Zombie Behaviour script attached 
prefab3 - Supply, this is a cube object with the pink material 

- Zombie spawner script is used to spawn x amount of zombies into the game, the zombie object used the zombie behavior script to dictate their motions, they detect how far away the nearest player is and can run faster or slower towards them based on how far away they are,

- Supply spawner script is used to 

- Agent spawner script is used to 


