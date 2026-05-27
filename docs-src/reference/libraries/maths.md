# maths

**Purpose:** small arithmetic and number helper library.

**Typical import:**

```novus
import lib/maths maths;
```

## Absolute value and sign

```novus
fn abs(x: i32) -> i32;
fn abs64(x: i64) -> i64;
fn sign(x: i32) -> i32;
fn sign64(x: i64) -> i64;
```

## Min / max / clamp

```novus
fn min(a: i32, b: i32) -> i32;
fn min64(a: i64, b: i64) -> i64;
fn max(a: i32, b: i32) -> i32;
fn max64(a: i64, b: i64) -> i64;
fn clamp(val: i32, lo: i32, hi: i32) -> i32;
fn clamp64(val: i64, lo: i64, hi: i64) -> i64;
fn wrap(val: i32, max_val: i32) -> i32;
```

## Integer utility functions

```novus
fn gcd(a: i32, b: i32) -> i32;
fn lcm(a: i32, b: i32) -> i32;
fn factorial(n: i32) -> i64;
fn fibonacci(n: i32) -> i64;
fn is_prime(n: i32) -> bool;
fn is_even(n: i32) -> bool;
fn is_odd(n: i32) -> bool;
fn digit_count(n: i32) -> i32;
fn digit_sum(n: i32) -> i32;
fn div_ceil(a: i32, b: i32) -> i32;
fn isqrt(n: i32) -> i32;
```

## Mapping and interpolation

```novus
fn lerp(a: i32, b: i32, t: i32) -> i32;
fn map_range(val: i32, in_min: i32, in_max: i32, out_min: i32, out_max: i32) -> i32;
```

## Powers

```novus
fn pow_i32(base: i32, exp: i32) -> i32;
fn pow_i64(base: i64, exp: i32) -> i64;
```
