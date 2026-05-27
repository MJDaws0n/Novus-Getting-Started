# env

**Purpose:** OS and process environment helpers.

**Typical import:**

```novus
import lib/env env;
```

## Identity and environment

```novus
fn get_username() -> str;
fn get_home_dir() -> str;
fn getenv(name: str) -> str;
fn gethostname() -> str;
fn getcwd() -> str;
```

## Process and user IDs

```novus
fn getpid() -> i32;
fn getppid() -> i32;
fn getuid() -> i32;
fn geteuid() -> i32;
```

## Platform information

```novus
fn get_arch() -> str;
fn get_os_name() -> str;
fn get_os_version() -> str;
```
