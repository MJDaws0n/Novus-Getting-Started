# net

**Purpose:** socket-level networking primitives.

**Typical import:**

```novus
import lib/net net;
```

## Socket setup and connection

- `net_socket`
- `net_bind`
- `net_listen`
- `net_listen_on`
- `net_accept`
- `net_connect`
- `net_connect_local`

## Socket options and process-level safety

- `net_set_reuse`
- `net_set_nonblock`
- `net_set_keepalive`
- `net_set_nosigpipe`
- `net_ignore_sigpipe`

## Read / write helpers

- `net_read`
- `net_read_safe`
- `net_read_line`
- `net_read_all`
- `net_write`
- `net_write_line`
- `net_write_str`

## Polling and connection state

- `net_poll_read`
- `net_bytes_available`
- `net_shutdown`
- `net_close`

## Buffer and address helpers

- `net_make_buf`
- `net_store8`
- `net_write_i16_be`
- `net_write_i32_le`
- `make_sockaddr_in`
- `make_sockaddr_in_addr`

## Windows startup / shutdown wrappers

- `net_wsa_startup`
- `net_wsa_cleanup`

