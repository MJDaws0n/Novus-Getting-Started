# window

--8<-- "includes/status-warning.md"


**Purpose:** native window creation, drawing, input polling, and platform/window-system glue.

**Typical import:**

```novus
import lib/window/main window;
```

## Main user-facing API

```novus
fn wm_open(title: str, exe_path: str, sock_path: str) -> i32;
fn wm_open_default(title: str) -> i32;
fn wm_show(fd: i32) -> i32;
fn wm_hide(fd: i32) -> i32;
fn wm_title(fd: i32, title: str) -> i32;
fn wm_resize(fd: i32, width: i32, height: i32) -> i32;
fn wm_size(fd: i32) -> str;
fn wm_quit(fd: i32) -> i32;
fn wm_ping(fd: i32) -> i32;
```

## Drawing

```novus
fn wm_clear(fd: i32, color: i32) -> i32;
fn wm_rect(fd: i32, x: i32, y: i32, width: i32, height: i32, color: i32) -> i32;
fn wm_present(fd: i32) -> i32;
```

## Input

```novus
fn wm_input(fd: i32) -> i32;
fn wm_input_left() -> i32;
fn wm_input_right() -> i32;
fn wm_input_jump() -> i32;
fn wm_input_down() -> i32;
fn wm_input_quit() -> i32;
```

## Process and helper startup

```novus
fn wm_start(sock_path: str) -> i32;
fn wm_start_auto(exe_path: str, sock_path: str, title: str) -> i32;
fn wm_spawn(exe_path: str, sock_path: str, title: str, auto_show: bool) -> i32;
fn wm_exe_default() -> str;
fn wm_sock_path_default() -> str;
fn wm_socket() -> i32;
fn wm_connect(sock_path: str) -> i32;
fn wm_sockaddr_un_make(path: str) -> str;
fn wm_sleep_ms(ms: i32) -> void;
```

## Command / protocol helpers

```novus
fn wm_send_cmd(fd: i32, cmd: str, arg: str) -> i32;
fn wm_send_line(fd: i32, line: str) -> i32;
fn wm_recv_line(fd: i32, buf_len: i32) -> str;
fn wm_recv_ok(fd: i32) -> str;
fn wm_escape_arg(arg: str) -> str;
fn wm_unescape_arg(arg: str) -> str;
fn wm_write_i32_le(buf: str, offset: i32, val: i32) -> void;
fn wm_to_u8(v: i32) -> i32;
```

## Browser / older helper protocol wrappers

```novus
fn wm_open_serve(title: str, root_dir: str, index_path: str) -> i32;
fn wm_serve(fd: i32, root_dir: str) -> str;
fn wm_jseval(fd: i32, code: str) -> i32;
fn wm_navigate(fd: i32, url: str) -> i32;
fn wm_send_to_js(fd: i32, msg: str) -> i32;
fn wm_recv_js_msg(fd: i32) -> str;
fn wm_parse_port(resp: str) -> i32;
fn wm_escape_js(s: str) -> str;
```

## Linux X11 and platform glue wrappers

```novus
fn init_x11(title: str) -> i32;
fn display_socket_path(display: str) -> str;
fn parse_display_num(display: str) -> i32;
fn read_xauthority_cookie(path: str, display_num: i32) -> str;
fn sock_socket(domain: i32, kind: i32) -> i32;
fn sock_connect(fd: i32, addr_ptr: u64, addr_len: i32) -> i32;
fn sys_close(fd: i32) -> void;
fn sys_read(fd: i32, addr: u64, count: i32) -> i32;
fn sys_write(fd: i32, addr: u64, count: i32) -> i32;
fn syscall_result_i32() -> i32;
fn syscall_result_i64() -> i64;
fn pad4(n: i32) -> i32;
fn read_u16_be(buf: str, off: i32) -> i32;
fn read_u16_le(buf: str, off: i32) -> i32;
fn read_u32_le(buf: str, off: i32) -> i32;
fn write_u16_be(buf: str, off: i32, val: i32) -> void;
fn write_u16_le(buf: str, off: i32, val: i32) -> void;
fn write_u32_le(buf: str, off: i32, val: i32) -> void;
fn write_all(fd: i32, data: str, count: i32) -> i32;
fn make_zero_buf(size: i32) -> str;
fn next_resource_id() -> i32;
fn process_x_message(pkt: str) -> void;
fn poll_x(timeout_ms: i32) -> i32;
```

## X11 drawing and resource wrappers

```novus
fn x_connect() -> i32;
fn x_setup(fd: i32) -> i32;
fn x_send_setup(fd: i32, cookie: str) -> i32;
fn x_read_setup(fd: i32) -> i32;
fn x_init_request_buffers() -> void;
fn x_intern_atom(name: str) -> i32;
fn x_create_window() -> i32;
fn x_map_window() -> void;
fn x_unmap_window() -> void;
fn x_resize_window(width: i32, height: i32) -> void;
fn x_set_title(title: str) -> void;
fn x_set_wm_protocols() -> void;
fn x_create_gc() -> void;
fn x_change_gc_color(color: i32) -> void;
fn x_create_pixmap(width: i32, height: i32) -> i32;
fn x_free_pixmap(pixmap_id: i32) -> void;
fn x_ensure_backbuffer() -> void;
fn x_copy_backbuffer_to_window() -> void;
fn x_fill_rect(x: i32, y: i32, w: i32, h: i32, color: i32) -> void;
fn x_drawable() -> i32;
fn x_sync() -> void;
fn x_file_open_read(path: str) -> i32;
fn x_file_seek(fd: i32, offset: u64, whence: i32) -> i64;
fn x_file_size(fd: i32) -> i32;
fn x_read_file(path: str) -> str;
fn x_pump_events() -> void;
fn x_set8(buf: str, off: i32, val: i32) -> void;
```

This is one of the widest APIs in the ecosystem because it contains both the public drawing API and a lot of transport/platform support code.
