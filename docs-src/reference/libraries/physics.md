# physics

--8<-- "includes/status-warning.md"


**Purpose:** lightweight game/simulation collision helpers.

**Typical import:**

```novus
import lib/physics/main physics;
```

## Collision

```novus
fn aabb_check(ax: i32, ay: i32, aw: i32, ah: i32, bx: i32, by: i32, bw: i32, bh: i32) -> i32;
```

This package is intentionally small in the current ecosystem and is mainly used by the platformer example.
