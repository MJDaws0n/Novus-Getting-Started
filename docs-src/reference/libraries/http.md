# http

**Purpose:** small HTTP server and response helper library.

**Typical import:**

```novus
import lib/http http;
```

## Listening and reading requests

- `http_listen`
- `http_accept`
- `http_read_request`
- `http_read_headers_only`
- `http_read_body_small`

## Request helpers

- `http_get_method`
- `http_get_path`
- `http_get_path_only`
- `http_get_query_string`
- `http_get_header`
- `http_get_body`
- `http_url_decode`

## Sending responses

- `http_send`
- `http_send_html`
- `http_send_json`
- `http_send_text`
- `http_send_404`
- `http_send_405`
- `http_send_500`
- `http_send_options`
- `http_serve_file`

## Formatting helpers

- `http_status_line`
- `http_content_type`
- `hex_digit_val`

## JSON helpers

- `json_escape`
- `json_get_value`
- `json_string`
- `json_object_1`
- `json_object_2`
- `json_object_3`

