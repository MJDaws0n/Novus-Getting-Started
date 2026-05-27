# smtp

--8<-- "includes/status-warning.md"


**Purpose:** lightweight SMTP email sending helpers.

**Typical import:**

```novus
import lib/smtp smtp;
```

## Sending mail

```novus
fn smtp_send_email(host: str, port: i32, username: str, password: str, from_email: str, to_email: str, subject: str, body: str) -> bool;
fn smtp_send_line(fd: i32, line: str) -> void;
```

## SMTP protocol helpers

```novus
fn smtp_read_response(fd: i32) -> str;
fn smtp_response_code(response: str) -> i32;
```

## Utility helpers

```novus
fn base64_encode(input: str) -> str;
fn parse_ip_octet(ip: str, index: i32) -> i32;
```
