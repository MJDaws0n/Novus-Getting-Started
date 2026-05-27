# time

**Purpose:** timing, elapsed-time measurement, and sleep helpers.

**Typical import:**

```novus
import lib/time time;
```

## Clock access

```novus
fn get_time_ms() -> i64;
fn get_time_s() -> i64;
fn get_time_us() -> i64;
```

## Elapsed-time helpers

```novus
fn elapsed_ms(start_ns: i64, end_ns: i64) -> i64;
fn elapsed_us(start_ns: i64, end_ns: i64) -> i64;
fn timer_start() -> i64;
fn timer_elapsed_ms(start: i64) -> i64;
fn timer_elapsed_s(start: i64) -> i64;
fn timer_elapsed_us(start: i64) -> i64;
```

## Sleep and formatting

```novus
fn sleep_ms(ms: i32) -> void;
fn sleep_s(seconds: i32) -> void;
fn format_duration_ms(ms: i64) -> str;
fn to_u8_time(v: i32) -> i32;
```
