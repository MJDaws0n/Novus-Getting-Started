# std

**Purpose:** standard language/runtime helpers used by almost every Novus app.

**Typical import:**

```novus
import lib/std std;
```

## Notes

- This page lists wrapper-style function families once.
- It does **not** expand every overload variant.

## Output and process control

- `print`
- `print_raw`
- `exit`

## Conversion families

- `to_str`
- `to_i32`
- `to_i64`
- `to_u64`
- `to_bool`
- `to_hex`

## Container helpers

- `len`
- `contains`

## String helpers

- `equals`
- `find`
- `last_find`
- `count`
- `is_empty`
- `is_blank`
- `lower`
- `upper`
- `reverse`
- `repeat`
- `trim`
- `trim_left`
- `trim_right`
- `pad_left`
- `pad_right`
- `replace`
- `replace_first`
- `split_first`
- `split_rest`

## Runtime and environment helpers

- `get_time_ns`
- `get_username`
- `get_home_dir`

## Memory wrappers

- `load8`
- `load32`
- `load64`
- `store_byte`

