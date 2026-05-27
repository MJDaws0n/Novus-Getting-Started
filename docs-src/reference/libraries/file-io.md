# file_io

--8<-- "includes/status-warning.md"


**Purpose:** file, directory, path, pipe, and memory-mapping helpers.

**Typical import:**

```novus
import lib/file_io fio;
```

## High-level convenience

```novus
fn read_file(path: str) -> str;
fn write_file(path: str, content: str) -> i32;
```

## File open / close / seek

```novus
fn file_open(path: str, flags: i32, mode: i32) -> i32;
fn file_open_read(path: str) -> i32;
fn file_open_write(path: str) -> i32;
fn file_close(fd: i32) -> void;
fn file_seek(fd: i32, offset: u64, whence: i32) -> i64;
fn file_size(fd: i32) -> u64;
```

## File reads and writes

```novus
fn file_read(fd: i32, buf_addr: u64, count: i32) -> i32;
fn file_write(fd: i32, buf_addr: u64, count: i32) -> i32;
fn file_write_str(fd: i32, s: str) -> i32;
fn file_append(path: str, content: str) -> i32;
```

## Existence and filesystem operations

```novus
fn file_exists(path: str) -> bool;
fn dir_exists(path: str) -> bool;
fn file_delete(path: str) -> i32;
fn file_copy(src_path: str, dst_path: str) -> i32;
fn file_rename(old_path: str, new_path: str) -> i32;
fn file_chdir(path: str) -> i32;
fn mkdirp(path: str) -> i32;
```

## Path helpers

```novus
fn path_join(a: str, b: str) -> str;
fn path_dir(path: str) -> str;
fn path_basename(path: str) -> str;
fn path_stem(path: str) -> str;
fn path_ext(path: str) -> str;
fn path_ext_no_dot(path: str) -> str;
fn path_insert_suffix(path: str, suffix: str) -> str;
```

## Pipe and descriptor helpers

```novus
fn pipe_create(res: []i32) -> void;
fn dup2(oldfd: i32, newfd: i32) -> void;
fn at_fdcwd() -> i32;
```

## Memory-mapped file helpers

```novus
fn file_mmap_read(fd: i32, size: u64) -> u64;
fn file_munmap(addr: u64, size: u64) -> void;
```

## Low-level syscall wrappers

```novus
fn sys_chmod(path: str, mode: i32) -> i32;
fn sys_mkdir(path: str, mode: i32) -> i32;
```
