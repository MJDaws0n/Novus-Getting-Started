# std

**Purpose:** standard language/runtime helpers used by almost every Novus app.

**Typical import:**

```novus
import lib/std std;
```

## Notes

- This page lists wrapper-style function families once.
- It does **not** expand every overload variant.
- The signatures below show the common forms you will usually call in app code.

## Output and process control

```novus
fn print(msg: str) -> void;
fn print_raw(msg: str) -> void;
fn exit(code: i32) -> void;
```

## Conversion families

```novus
fn to_str(n: i32) -> str;
fn to_str(n: i64) -> str;
fn to_str(b: bool) -> str;
fn to_str(s: str) -> str;

fn to_i32(s: str) -> i32;
fn to_i32(n: i64) -> i32;
fn to_i32(n: u64) -> i32;
fn to_i32(n: i32) -> i32;

fn to_i64(s: str) -> i64;
fn to_i64(n: i32) -> i64;
fn to_i64(n: u64) -> i64;
fn to_i64(n: i64) -> i64;

fn to_u64(n: i32) -> u64;
fn to_u64(n: i64) -> u64;
fn to_u64(n: u64) -> u64;

fn to_bool(s: str) -> bool;
fn to_bool(b: bool) -> bool;

fn to_hex(n: i32) -> str;
```

## Container helpers

```novus
fn len(s: str) -> i32;
fn len(arr: []i32) -> i32;
fn len(arr: []i64) -> i32;
fn len(arr: []u64) -> i32;
fn len(arr: []str) -> i32;

fn contains(s: str, needle: str) -> bool;
fn contains(arr: []i32, v: i32) -> bool;
fn contains(arr: []i64, v: i64) -> bool;
fn contains(arr: []str, v: str) -> bool;
```

## String helpers

```novus
fn equals(a: str, b: str) -> bool;
fn find(s: str, needle: str) -> i32;
fn last_find(s: str, needle: str) -> i32;
fn count(s: str, needle: str) -> i32;
fn is_empty(s: str) -> bool;
fn is_blank(s: str) -> bool;
fn lower(s: str) -> str;
fn upper(s: str) -> str;
fn reverse(s: str) -> str;
fn repeat(s: str, n: i32) -> str;
fn trim(s: str) -> str;
fn trim_left(s: str) -> str;
fn trim_right(s: str) -> str;
fn pad_left(s: str, total: i32, pad: str) -> str;
fn pad_right(s: str, total: i32, pad: str) -> str;
fn replace(s: str, old_val: str, new_val: str) -> str;
fn replace_first(s: str, old_val: str, new_val: str) -> str;
fn split_first(s: str, delim: str) -> str;
fn split_rest(s: str, delim: str) -> str;
```

## Runtime and environment helpers

```novus
fn get_time_ns() -> i64;
fn get_username() -> str;
fn get_home_dir() -> str;
```

## Memory wrappers

```novus
fn load8(addr: u64) -> i32;
fn load32(addr: u64) -> i32;
fn load64(addr: u64) -> i64;
fn store_byte(addr: u64, value: i32) -> void;
```

## Backward-compat typed names

Older projects may still use the pre-unified names such as `i32_to_str`, `str_to_i32`, `array_len_i64`, `str_trim`, or `str_contains`. Newer code should prefer the unified wrapper names above.
