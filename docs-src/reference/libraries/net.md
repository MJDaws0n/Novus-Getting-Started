# net

--8<-- "includes/status-warning.md"


**Purpose:** socket-level networking primitives.

**Typical import:**

```novus
import lib/net net;
```

## Socket setup and connection

```novus
fn net_socket() -> i32;
fn net_bind(fd: i32, port: i32) -> i32;
fn net_listen(fd: i32, backlog: i32) -> i32;
fn net_listen_on(port: i32, backlog: i32) -> i32;
fn net_accept(fd: i32) -> i32;
fn net_connect(fd: i32, a: i32, b: i32, c: i32, d: i32, port: i32) -> i32;
fn net_connect_local(port: i32) -> i32;
```

## Socket options and process-level safety

```novus
fn net_set_reuse(fd: i32) -> i32;
fn net_set_nonblock(fd: i32) -> i32;
fn net_set_keepalive(fd: i32) -> i32;
fn net_set_nosigpipe(fd: i32) -> i32;
fn net_ignore_sigpipe() -> void;
```

## Read / write helpers

```novus
fn net_read(fd: i32, buf: str, max_len: i32) -> i32;
fn net_read_safe(fd: i32, buf: str, max_len: i32) -> i32;
fn net_read_line(fd: i32, max_len: i32) -> str;
fn net_read_all(fd: i32, max_len: i32) -> str;
fn net_write(fd: i32, data: str, length: i32) -> i32;
fn net_write_line(fd: i32, s: str) -> i32;
fn net_write_str(fd: i32, s: str) -> i32;
```

## Polling and connection state

```novus
fn net_poll_read(fd: i32, timeout_ms: i32) -> i32;
fn net_bytes_available(fd: i32) -> i32;
fn net_shutdown(fd: i32, how: i32) -> i32;
fn net_close(fd: i32) -> void;
```

## Buffer and address helpers

```novus
fn net_make_buf(size: i32) -> str;
fn net_store8(addr: u64, val: i32) -> void;
fn net_write_i16_be(buf: str, offset: i32, val: i32) -> void;
fn net_write_i32_le(buf: str, offset: i32, val: i32) -> void;
fn make_sockaddr_in(port: i32) -> str;
fn make_sockaddr_in_addr(a: i32, b: i32, c: i32, d: i32, port: i32) -> str;
fn to_u8_net(v: i32) -> i32;
```

## Windows startup / shutdown wrappers

```novus
fn net_wsa_startup() -> i32;
fn net_wsa_cleanup() -> void;
```
