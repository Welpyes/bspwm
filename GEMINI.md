# bspwm - Binary Space Partitioning Window Manager

`bspwm` is a tiling window manager that represents windows as the leaves of a full binary tree. This specific version includes modifications for rounded corners using the Xshape extension.

## Project Overview

- **Core Architecture:** Windows are managed in a binary tree. Monitors contain desktops, and each desktop has its own tree.
- **Client-Server Model:** `bspwm` acts as the server, and `bspc` is the CLI client that communicates with it over a Unix socket.
- **Input Handling:** `bspwm` does not handle keyboard or pointer inputs directly. It relies on a third-party daemon like `sxhkd` to translate inputs into `bspc` commands.
- **Main Technologies:** C99, XCB (X C Binding), Xshape extension.

## Building and Running

### Build Commands
- **Build all:** `make`
- **Debug build:** `make debug`
- **Clean:** `make clean`
- **Install:** `sudo make install` (Default prefix is `/usr/local`)

### Dependencies
Requires `xcb`, `xcb-util`, `xcb-keysyms`, `xcb-icccm`, `xcb-ewmh`, `xcb-randr`, `xcb-xinerama`, and `xcb-shape`.

### Running
`bspwm` is typically started from an `.xinitrc` file or a display manager. It looks for its configuration file at `$XDG_CONFIG_HOME/bspwm/bspwmrc`, which is a shell script that uses `bspc` to configure the window manager.

## Testing

Tests are located in the `tests/` directory.
- **Requirement:** `jshon` must be installed.
- **Execution:** 
  1. Build the project: `make`
  2. Run the test suite: `./tests/run`

## Development Conventions

- **Language:** C99 (`-std=c99`).
- **Style:** Pedantic, strict warnings (`-Wall -Wextra -pedantic`).
- **State Management:** Core state is maintained in `src/bspwm.h` (externs) and defined in `src/types.h`.
- **Communication:** Uses a custom message format parsed by `src/messages.c` and `src/parse.c`.

## Key Files and Directories

- `src/`: Core source code.
  - `bspwm.c`: Main entry point and event loop.
  - `bspc.c`: Source for the CLI client.
  - `tree.c`: Binary tree management logic.
  - `types.h`: Core data structures (Monitor, Desktop, Node, Client).
- `examples/`: Sample configuration files for `bspwm` and `sxhkd`.
- `doc/`: Documentation, including man pages and changelogs.
- `contrib/`: Shell completions and desktop files.

## Rounded Corners Modification

This version supports the following additional configuration options via `bspc`:
- `bspc config border_radius <int>`: Sets the radius for rounded corners.
- `bspc config fill_border <bool>`: If true, rounds the window without cutting the border.
