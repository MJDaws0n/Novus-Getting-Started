# process

--8<-- "includes/status-warning.md"


**Purpose:** subprocess launching, output capture, waiting, and a few desktop picker helpers.

**Typical import:**

```novus
import lib/process/main process;
```

## Running commands

```novus
fn run_cmd(exe: str, argv: []u64) -> i32;
fn shell_exec(cmd: str) -> i32;
fn shell_output(cmd: str, max_len: i32) -> str;
```

## Capturing output

```novus
fn capture_output(exe: str, argv: []u64, max_len: i32) -> str;
fn capture_output_full(exe: str, argv: []u64, max_len: i32) -> str;
```

## Waiting

```novus
fn wait_pid(pid: i32) -> i32;
fn waitpid_nohang() -> void;
```

## UI picker helpers

```novus
fn pick_file_dialog(file_type: str) -> str;
fn pick_folder_dialog() -> str;
```
