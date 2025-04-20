# cub3d

A 3D maze game inspired by Wolfenstein 3D, developed using raycasting techniques and the MiniLibX graphics library.

## Table of Contents
- [cub3d](#cub3d)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Requirements](#requirements)
  - [Installation](#installation)
  - [Controls](#controls)
  - [Map Format](#map-format)
    - [Texture Configuration](#texture-configuration)
    - [Floor and Ceiling Colors](#floor-and-ceiling-colors)
    - [Map Layout](#map-layout)
  - [Implementation Details](#implementation-details)
    - [Raycasting](#raycasting)
    - [Movement and Collision](#movement-and-collision)
  - [Project Structure](#project-structure)

## Overview

cub3d is a first-person 3D maze navigator that renders a 3D perspective using raycasting techniques. The project is inspired by the groundbreaking game Wolfenstein 3D and demonstrates fundamental principles of computer graphics such as ray-tracing, texture mapping, and 3D projection.

## Features

- First-person 3D perspective rendered using raycasting
- Textured walls with directional textures (North, South, East, West)
- Customizable floor and ceiling colors
- Smooth movement and rotation controls
- Collision detection with walls
- Custom map loading from .cub files

## Requirements

- macOS or Linux
- MiniLibX graphics library
- C compiler (gcc/clang)
- make

## Installation

1. Clone the repository
```bash
git clone <repository-url>
cd cub3d
```

2. Compile the game
```bash
make
```

3. Run the game with a valid map
```bash
./cub3d maps/map.cub
```

## Controls

- **W**: Move forward
- **S**: Move backward
- **A**: Strafe left
- **D**: Strafe right
- **←**: Rotate camera left
- **→**: Rotate camera right
- **ESC**: Exit the game

## Map Format

Maps for cub3d must be stored in files with the `.cub` extension. The map file should include:

### Texture Configuration
Each texture is specified with a directional identifier followed by the path to the texture file:
```
NO textures/north_texture.xpm
SO textures/south_texture.xpm
WE textures/west_texture.xpm
EA textures/east_texture.xpm
```

### Floor and Ceiling Colors
Colors are specified with RGB values (0-255):
```
F 220,100,0    # Floor color
C 225,30,0     # Ceiling color
```

### Map Layout
The map layout uses the following characters:
- **0**: Empty space (where the player can move)
- **1**: Wall
- **N/S/E/W**: Player starting position and orientation (only one allowed)
- **Space**: Can be used for spacing, treated as outside the map bounds

Example of a valid map:
```
        1111111111111111111111111
        1000000000110000000000001
        1011000001110000000000001
        1001000000000000000000001
111111111011000001110000000000001
100000000011000001110111111111111
11110111111111011100000010001
11110111111111011101010010001
11000000110101011100000010001
10000000000000001100000010101
10000000000000001101010010001
11000001110101011111011110N0111
```

The map must be surrounded by walls to be valid.

## Implementation Details

### Raycasting

The game uses raycasting to create a 3D perspective view:

1. For each vertical screen column:
   - Calculate the ray direction from the player's position
   - Determine where the ray hits a wall using the Digital Differential Analysis (DDA) algorithm
   - Calculate the perpendicular distance to the wall to avoid fisheye effect
   - Determine the height of the wall slice to draw

2. Texturing:
   - Calculate which part of the texture to display based on where the ray hit the wall
   - Apply the appropriate texture (North, South, East, or West) based on which wall was hit
   - Draw the textured wall slice at the appropriate position

### Movement and Collision

- Player movement is calculated using vector operations
- Collision detection prevents moving through walls
- Camera rotation is handled by rotating both the direction and plane vectors

## Project Structure

- **main.c**: Entry point and game loop
- **control/**: Player movement and keyboard input handling
- **exit/**: Clean exit and resource management
- **get_next_line/**: File reading utility
- **includes/**: Header files
  - **config.h**: Game configuration constants
  - **controllers.h**: Input handling definitions
  - **dda.h**: Raycasting algorithm declarations
  - **map.h**: Map data structures and utilities
  - **player.h**: Player state and movement
  - **render.h**: Rendering declarations
  - **vector.h**: Vector operations
- **libft/**: Custom library with utility functions
- **memory-allocator/**: Memory management utilities
- **minilibx/**: Graphics library for rendering
- **parser/**: Map file parsing
- **render/**: Raycasting and rendering implementation
- **textures/**: Game assets in XPM format

---

*This project is part of the 42 School curriculum.*