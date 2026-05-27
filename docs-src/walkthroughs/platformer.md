# Building the platformer

--8<-- "includes/status-warning.md"


The [platformer-game](https://github.com/MJDaws0n/platformer-game) is one of the best current examples of a real Novus app that is still small enough to understand in one sitting.

## What it imports

```novus
import lib/window/main window;
import lib/physics/main physics;
import lib/std/main;
```

That already tells you a lot about the architecture:

- `window` handles native windowing and drawing
- `physics` handles collision checks
- `std` provides general helpers

## Game state

The project stores almost all state in globals:

- player position and velocity
- grounded state
- camera position
- life count
- current mode (playing / win / lose)
- current view size

That is a very common early-stage Novus pattern: keep the app simple, obvious, and mostly data-driven.

## Resizing and view size

The platformer asks the window library for the current content size:

```novus
fn update_view_size(fd: i32) -> void {
    let size: str = window.wm_size(fd);
    let sep: i32 = str_find(size, "x");
    if (sep < 0) { return; }
    let w: i32 = str_to_i32(substr_len(size, 0, sep));
    let h: i32 = str_to_i32(substr(size, sep + 1));
    if (w >= 320) { view_width = w; }
    if (h >= 240) { view_height = h; }
}
```

That is what lets the game expand the visible play area instead of just stretching pixels.

## Update loop

The logic loop is straightforward:

```novus
fn update_game(input_mask: i32) -> void {
    frame_index = frame_index + 1;

    if ((input_mask & window.wm_input_quit()) != 0) {
        app_running = 0;
        return;
    }

    if (game_mode != 0) {
        if ((input_mask & window.wm_input_jump()) != 0) {
            restart_game();
        }
        return;
    }

    apply_input(input_mask);
    update_player();
}
```

Important design point: the game treats input as a bitmask, not as individual callback events.

## Rendering model

Rendering is explicit rectangle drawing.

```novus
fn render_game(fd: i32) -> void {
    window.wm_clear(fd, COLOR_SKY());
    draw_world(fd);
    draw_hud(fd);
    window.wm_present(fd);
}
```

That is the core frame model:

1. clear
2. draw the world
3. draw the HUD
4. present

## Clipping

The project clips every rectangle against the current view size before it reaches the window backend:

```novus
fn draw_rect_clipped(fd: i32, x: i32, y: i32, width: i32, height: i32, color: i32) -> void {
    ...
    if (draw_x + draw_w > VIEW_WIDTH()) {
        draw_w = VIEW_WIDTH() - draw_x;
    }
    if (draw_y + draw_h > VIEW_HEIGHT()) {
        draw_h = VIEW_HEIGHT() - draw_y;
    }
    ...
    window.wm_rect(fd, draw_x, draw_y, draw_w, draw_h, color);
}
```

This is a good example of keeping high-level game logic independent from backend details.

## Main loop

```novus
fn main() -> i32 {
    let fd: i32 = window.wm_open_default("Novus Platformer");
    if (fd < 0) {
        return 1;
    }

    window.wm_resize(fd, VIEW_WIDTH(), VIEW_HEIGHT());
    window.wm_show(fd);
    update_view_size(fd);
    restart_game();

    while (app_running == 1) {
        let input_mask: i32 = window.wm_input(fd);
        update_view_size(fd);
        update_game(input_mask);
        render_game(fd);
        window.wm_sleep_ms(16);
    }

    window.wm_quit(fd);
    return 0;
}
```

This is a strong example of the normal shape of a Novus application:

- initialise libraries
- run a simple main loop
- keep rendering explicit
- clean up on exit

## Why this example matters

The platformer demonstrates:

- package-based imports
- a native window API
- drawing without a heavyweight graphics stack
- real input handling
- a simple game loop
- resize-aware rendering

If you want to learn how Novus applications are *really* put together, study this repo after you are comfortable with the basics.

