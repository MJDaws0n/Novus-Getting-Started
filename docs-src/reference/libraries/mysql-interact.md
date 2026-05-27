# MySQL-Interact

**Purpose:** MySQL client and query helper library.

**Typical import:**

```novus
import lib/MySQL-Interact/main mysql;
```

This package is much broader than the others because it includes both high-level query helpers and lower-level packet/protocol utilities.

## Connection and session

```novus
fn mysql_connect(a: i32, b: i32, c: i32, d: i32, port: i32, user: str, password: str, database: str) -> i32;
fn mysql_connect_local(port: i32, user: str, password: str, database: str) -> i32;
fn mysql_close(fd: i32) -> void;
fn mysql_ping(fd: i32) -> bool;
fn mysql_use_db(fd: i32, database: str) -> str;
fn mysql_server_version(fd: i32) -> str;
fn mysql_current_database(fd: i32) -> str;
fn mysql_current_user(fd: i32) -> str;
```

## Query execution

```novus
fn mysql_query(fd: i32, sql: str) -> str;
fn mysql_exec(fd: i32, sql: str) -> bool;
fn mysql_query_scalar(fd: i32, sql: str) -> str;
fn mysql_query_row(fd: i32, sql: str) -> str;
```

## Result inspection

```novus
fn mysql_is_error(result: str) -> bool;
fn mysql_is_ok(result: str) -> bool;
fn mysql_is_result_set(result: str) -> bool;
fn mysql_error_msg(result: str) -> str;
fn mysql_error_code(result: str) -> i32;
fn mysql_affected_rows(result: str) -> i64;
fn mysql_insert_id(result: str) -> i64;
fn mysql_num_cols(result: str) -> i32;
fn mysql_num_rows(result: str) -> i32;
fn mysql_col_name(result: str, col: i32) -> str;
fn mysql_get(result: str, row: i32, col: i32) -> str;
fn mysql_is_null(result: str, row: i32, col: i32) -> bool;
```

## Escaping and quoting

```novus
fn mysql_escape(s: str) -> str;
fn mysql_quote(s: str) -> str;
fn mysql_escape_id(s: str) -> str;
```

## Prepared statements and parameters

```novus
fn mysql_prepare(fd: i32, sql: str) -> i32;
fn mysql_params_new(count: i32) -> str;
fn my_params_end(params: str) -> i32;
fn mysql_bind_str(params: str, index: i32, value: str) -> str;
fn mysql_bind_i32(params: str, index: i32, value: i32) -> str;
fn mysql_bind_null(params: str, index: i32) -> str;
fn mysql_stmt_execute(fd: i32, stmt_id: i32, params: str, num_params: i32) -> str;
fn mysql_stmt_close(fd: i32, stmt_id: i32) -> void;
fn mysql_stmt_reset(fd: i32, stmt_id: i32) -> bool;
fn mysql_set_param_str(sql: str, val: str) -> str;
fn mysql_set_param_i32(sql: str, val: i32) -> str;
fn mysql_set_param_i64(sql: str, val: i64) -> str;
fn mysql_set_param_null(sql: str) -> str;
```

## Transactions

```novus
fn mysql_begin(fd: i32) -> str;
fn mysql_commit(fd: i32) -> str;
fn mysql_rollback(fd: i32) -> str;
fn mysql_autocommit_on(fd: i32) -> str;
fn mysql_autocommit_off(fd: i32) -> str;
```

## Schema and discovery helpers

```novus
fn mysql_list_databases(fd: i32) -> str;
fn mysql_list_tables(fd: i32) -> str;
fn mysql_table_exists(fd: i32, table: str) -> bool;
```

## Packet, buffer, and protocol helpers

```novus
fn my_to_i64(x: i32) -> i64;
fn my_to_i32(x: i64) -> i32;
fn my_buf_copy(dst: str, dst_off: i32, src: str, src_off: i32, count: i32) -> void;
fn my_extract(src: str, off: i32, count: i32) -> str;
fn my_buf_set(dst: str, off: i32, val: i32) -> void;
fn my_buf_get(src: str, off: i32) -> i32;
fn my_read_u16(buf: str, off: i32) -> i32;
fn my_read_u32(buf: str, off: i32) -> i64;
fn my_write_u16(buf: str, off: i32, val: i32) -> void;
fn my_write_u24(buf: str, off: i32, val: i32) -> void;
fn my_write_u32(buf: str, off: i32, val: i64) -> void;
fn my_write_cstr(buf: str, off: i32, s: str) -> i32;
fn my_read_cstr(buf: str, off: i32) -> str;
fn my_cstr_len(buf: str, off: i32) -> i32;
fn my_read_lenenc_val(buf: str, off: i32) -> i64;
fn my_lenenc_size(buf: str, off: i32) -> i32;
fn my_read_exact(fd: i32, length: i32) -> str;
fn mysql_read_packet(fd: i32) -> str;
fn mysql_write_packet(fd: i32, seq: i32, data: str, data_len: i32) -> void;
fn my_pkt_len(pkt: str) -> i32;
fn my_pkt_byte(pkt: str, off: i32) -> i32;
fn my_sep() -> str;
fn my_row_sep() -> str;
fn my_null_marker() -> str;
fn my_parse_ok(pkt: str) -> str;
fn my_parse_err(pkt: str) -> str;
```
