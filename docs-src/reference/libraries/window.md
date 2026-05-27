# window

**Purpose:** native window creation, drawing, input polling, and platform/window-system glue.

**Typical import:**

```novus
import lib/window/main window;
```

## Main user-facing API

- `wm_open`
- `wm_open_default`
- `wm_show`
- `wm_hide`
- `wm_title`
- `wm_resize`
- `wm_size`
- `wm_quit`
- `wm_ping`

## Drawing

- `wm_clear`
- `wm_rect`
- `wm_present`

## Input

- `wm_input`
- `wm_input_left`
- `wm_input_right`
- `wm_input_jump`
- `wm_input_down`
- `wm_input_quit`

## Process and helper startup

- `wm_start`
- `wm_start_auto`
- `wm_spawn`
- `wm_exe_default`
- `wm_sock_path_default`
- `wm_socket`
- `wm_connect`
- `wm_sockaddr_un_make`
- `wm_sleep_ms`

## Command / protocol helpers

- `wm_send_cmd`
- `wm_send_line`
- `wm_recv_line`
- `wm_recv_ok`
- `wm_escape_arg`
- `wm_unescape_arg`
- `wm_write_i32_le`
- `wm_to_u8`

## Browser / older helper protocol wrappers

- `wm_open_serve`
- `wm_serve`
- `wm_jseval`
- `wm_navigate`
- `wm_send_to_js`
- `wm_recv_js_msg`
- `wm_parse_port`
- `wm_escape_js`

## Linux X11 and platform glue wrappers

- `init_x11`
- `display_socket_path`
- `parse_display_num`
- `read_xauthority_cookie`
- `sock_socket`
- `sock_connect`
- `sys_close`
- `sys_read`
- `sys_write`
- `syscall_result_i32`
- `syscall_result_i64`
- `pad4`
- `read_u16_be`
- `read_u16_le`
- `read_u32_le`
- `write_u16_be`
- `write_u16_le`
- `write_u32_le`
- `write_all`
- `make_zero_buf`
- `next_resource_id`
- `process_x_message`
- `poll_x`

## X11 drawing and resource wrappers

- `x_connect`
- `x_setup`
- `x_send_setup`
- `x_read_setup`
- `x_init_request_buffers`
- `x_intern_atom`
- `x_create_window`
- `x_map_window`
- `x_unmap_window`
- `x_resize_window`
- `x_set_title`
- `x_set_wm_protocols`
- `x_create_gc`
- `x_change_gc_color`
- `x_create_pixmap`
- `x_free_pixmap`
- `x_ensure_backbuffer`
- `x_copy_backbuffer_to_window`
- `x_fill_rect`
- `x_drawable`
- `x_sync`
- `x_file_open_read`
- `x_file_seek`
- `x_file_size`
- `x_read_file`
- `x_pump_events`
- `x_set8`

This is one of the widest APIs in the ecosystem because it contains both the public drawing API and a lot of transport/platform support code.

