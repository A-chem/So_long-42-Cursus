# So_long - 42 Cursus

A 2D top-down game written in C with MiniLibX, developed as part of the 42 School curriculum.

## Project Overview

So_long is a graphical programming project that introduces the fundamentals of 2D game development in C. The application loads a tile-based map from a `.ber` file, validates its structure, renders it through MiniLibX, and allows the player to explore the level, collect every item, and reach the exit.

The project combines file parsing, map validation, flood-fill path checking, event-driven input, graphical rendering, game-state management, and dynamic memory handling.

This repository includes both the mandatory implementation and the bonus implementation.

## Features

### Mandatory version

- Loads maps from `.ber` files.
- Validates the map before launching the game.
- Ensures that the map is rectangular and enclosed by walls.
- Verifies the required map components:
  - Exactly one player, represented by `P`.
  - At least one collectible, represented by `C`.
  - Exactly one exit, represented by `E`.
- Uses flood fill to confirm that all collectibles and the exit are reachable.
- Renders the map using MiniLibX.
- Supports player movement with `W`, `A`, `S`, and `D`.
- Counts and displays the number of player moves.
- Prevents movement through walls.
- Ends the game after all collectibles have been gathered and the exit is reached.
- Supports clean termination with the Escape key or by closing the game window.

### Bonus version

The bonus implementation extends the base game with additional gameplay elements:

- Moving enemies represented by `N` on the map.
- Enemy movement controlled by the MiniLibX game loop.
- Horizontal and vertical enemy movement behavior.
- Collision detection between the player and enemies.
- A game-over state when an enemy catches the player.
- Additional rendering and image-loading logic.
- Player animation support for horizontal movement.
- Enhanced map examples and gameplay presentation.

## Map Format

Maps use the `.ber` extension and are represented as a grid of characters. Each character corresponds to a tile:

| Symbol | Meaning |
|:------:|---------|
| `1` | Wall |
| `0` | Empty floor |
| `P` | Player starting position |
| `C` | Collectible |
| `E` | Exit |
| `N` | Enemy, bonus version only |

Example map:

```text
111111111111
100000000001
100C0000C001
100000P00001
100000000E01
111111111111
```

A valid map must be rectangular, completely surrounded by walls, contain one player and one exit, include at least one collectible, and provide a valid path allowing the player to collect every item before reaching the exit.

## Core Concepts

- File parsing with a custom `get_next_line` implementation.
- Map validation and error handling.
- Flood-fill reachability analysis.
- Graphical rendering with MiniLibX.
- Keyboard and window event handling.
- Player movement and move counting.
- Game-state management.
- Dynamic memory allocation and cleanup.
- Linked-list management for bonus enemies.
- Game loops and collision detection.
- Strict compilation with `-Wall -Wextra -Werror`.

## Repository Structure

```text
.
├── Mandatory              Required version of the project
│   ├── so_long.c          Program entry point and initialization
│   ├── check_map.c        Map validation
│   ├── flood_fill.c       Reachability validation
│   ├── draw_map.c         Mandatory rendering
│   ├── events.c           Keyboard and player movement
│   ├── move_count.c       Move counter display
│   ├── free_data.c        Resource cleanup
│   ├── get_next_line*.c   Line-by-line file reading
│   └── *.h                Headers and data structures
├── Bonus                   Extended version with enemies and animations
│   ├── so_long_bonus.c
│   ├── check_map_bonus.c
│   ├── flood_fill_bonus.c
│   ├── render_map_bonus.c
│   ├── events_bonus.c
│   ├── enemy_bonus.c
│   ├── move_enemy_bonus.c
│   ├── load_img_bonus.c
│   └── *.h
├── maps                    Example `.ber` maps
├── textures                Game textures and assets
├── Makefile                Build and cleanup commands
└── Subject.pdf             42 project subject
```

## Requirements

- A Unix-like operating system.
- A C compiler such as `cc` or `clang`.
- `make`.
- MiniLibX installed and available to the linker.
- On macOS, the OpenGL and AppKit frameworks.

The current Makefile links MiniLibX with the following options:

```text
-lmlx -framework OpenGL -framework AppKit
```

MiniLibX setup can vary depending on the operating system. On Linux, the linker flags and system dependencies may need to be adapted to the local MiniLibX installation.

## Build and Run

Clone the repository and enter the project directory:

```bash
git clone https://github.com/A-chem/So_long-42-Cursus.git
cd So_long-42-Cursus
```

### Build the mandatory version

```bash
make
```

Run the mandatory version:

```bash
./so_long maps/map.ber
```

### Build the bonus version

```bash
make bonus
```

Run the bonus version:

```bash
./so_long_bonus maps/map_bonus.ber
```

### Clean build files

```bash
make clean
make fclean
make re
```

The commands perform the following operations:

- `make clean` removes object files.
- `make fclean` removes object files and executables.
- `make re` rebuilds the mandatory version from scratch.

## Controls

| Key | Action |
|:---:|--------|
| `W` | Move up |
| `A` | Move left |
| `S` | Move down |
| `D` | Move right |
| `Esc` | Exit the game |

The player must collect every `C` before the `E` exit becomes usable. In the bonus version, the player must also avoid moving enemies.

## Game Flow

1. The program receives a `.ber` map path as its command-line argument.
2. The map is read and converted into an internal grid.
3. The map is checked for valid dimensions, borders, characters, and required entities.
4. Flood fill confirms that all collectibles and the exit are reachable.
5. MiniLibX creates the game window and renders the initial state.
6. Keyboard events update the player position and move counter.
7. The mandatory version ends when the player reaches the exit after collecting all items.
8. The bonus version updates enemies through the game loop and ends on enemy collision or successful completion.
9. All allocated resources are released before termination.

## Error Handling

The program rejects invalid input and safely terminates when it encounters problems such as:

- Missing or malformed map files.
- Incorrect file extensions.
- Non-rectangular maps.
- Open map borders.
- Invalid characters.
- Missing or duplicated player or exit positions.
- Unreachable collectibles or exit paths.
- Allocation or initialization failures.

## Learning Outcomes

This project provides practical experience with:

- C programming and modular project organization.
- Low-level graphical programming with MiniLibX.
- Keyboard and window event callbacks.
- Two-dimensional grid algorithms and flood-fill traversal.
- Structured input-file parsing.
- Dynamic memory allocation and cleanup.
- Linked-list management for bonus enemies.
- Game loops, collision detection, and state transitions.
- Debugging and defensive error handling.
- Writing code that passes strict compiler warnings.

## 42 Project Context

So_long is part of the 42 Cursus and is designed to reinforce the transition from command-line programs to interactive graphical applications. The project requires the developer to design the complete data flow from map input to rendering while ensuring that every possible map state is validated before gameplay begins.

The original project requirements are available in [Subject.pdf](./Subject.pdf).

## Project Status

- Mandatory implementation included.
- Bonus implementation included.
- Example maps and textures included.
- Build automation provided through the Makefile.

## Author

Developed by [A-chem](https://github.com/A-chem) as part of the 42 Cursus.

## License

No license file is currently included in this repository. Unless a license is added, the project should be treated as source-available for educational and reference purposes only.
