# file_io

**Purpose:** file, directory, path, pipe, and memory-mapping helpers.

**Typical import:**

```novus
import lib/file_io fio;
```

## High-level convenience

- `read_file`
- `write_file`

## File open / close / seek

- `file_open`
- `file_open_read`
- `file_open_write`
- `file_close`
- `file_seek`
- `file_size`

## File reads and writes

- `file_read`
- `file_write`
- `file_write_str`
- `file_append`

## Existence and filesystem operations

- `file_exists`
- `dir_exists`
- `file_delete`
- `file_copy`
- `file_rename`
- `file_chdir`
- `mkdirp`

## Path helpers

- `path_join`
- `path_dir`
- `path_basename`
- `path_stem`
- `path_ext`
- `path_ext_no_dot`
- `path_insert_suffix`

## Pipe and descriptor helpers

- `pipe_create`
- `dup2`
- `at_fdcwd`

## Memory-mapped file helpers

- `file_mmap_read`
- `file_munmap`

## Low-level syscall wrappers

- `sys_chmod`
- `sys_mkdir`

