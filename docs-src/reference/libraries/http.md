# http

--8<-- "includes/status-warning.md"


**Purpose:** small HTTP server and response helper library.

**Typical import:**

```novus
import lib/http http;
```

## Listening and reading requests

```novus
fn http_listen(port: i32) -> i32;
fn http_accept(server_fd: i32) -> i32;
fn http_read_request(client_fd: i32) -> str;
fn http_read_headers_only(client_fd: i32) -> str;
fn http_read_body_small(client_fd: i32, content_length: i32) -> str;
```

## Request helpers

```novus
fn http_get_method(request: str) -> str;
fn http_get_path(request: str) -> str;
fn http_get_path_only(path: str) -> str;
fn http_get_query_string(path: str) -> str;
fn http_get_header(request: str, name: str) -> str;
fn http_get_body(request: str) -> str;
fn http_url_decode(s: str) -> str;
```

## Sending responses

```novus
fn http_send(client_fd: i32, status_code: i32, status_text: str, content_type: str, body: str) -> void;
fn http_send_html(client_fd: i32, html: str) -> void;
fn http_send_json(client_fd: i32, json: str) -> void;
fn http_send_text(client_fd: i32, text: str) -> void;
fn http_send_404(client_fd: i32) -> void;
fn http_send_405(client_fd: i32) -> void;
fn http_send_500(client_fd: i32, msg: str) -> void;
fn http_send_options(client_fd: i32) -> void;
fn http_serve_file(client_fd: i32, file_path: str) -> void;
```

## Formatting helpers

```novus
fn http_status_line(code: i32) -> str;
fn http_content_type(path: str) -> str;
fn hex_digit_val(ch: i32) -> i32;
```

## JSON helpers

```novus
fn json_escape(s: str) -> str;
fn json_get_value(json: str, key: str) -> str;
fn json_string(key: str, value: str) -> str;
fn json_object_1(k1: str, v1: str) -> str;
fn json_object_2(k1: str, v1: str, k2: str, v2: str) -> str;
fn json_object_3(k1: str, v1: str, k2: str, v2: str, k3: str, v3: str) -> str;
```
