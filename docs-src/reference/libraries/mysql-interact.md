# MySQL-Interact

**Purpose:** MySQL client and query helper library.

**Typical import:**

```novus
import lib/MySQL-Interact/main mysql;
```

This package is much broader than the others because it includes both high-level query helpers and lower-level packet/protocol utilities.

## Connection and session

- `mysql_connect`
- `mysql_connect_local`
- `mysql_close`
- `mysql_ping`
- `mysql_use_db`
- `mysql_server_version`
- `mysql_current_database`
- `mysql_current_user`

## Query execution

- `mysql_query`
- `mysql_exec`
- `mysql_query_scalar`
- `mysql_query_row`

## Result inspection

- `mysql_is_error`
- `mysql_is_ok`
- `mysql_is_result_set`
- `mysql_error_msg`
- `mysql_error_code`
- `mysql_affected_rows`
- `mysql_insert_id`
- `mysql_num_cols`
- `mysql_num_rows`
- `mysql_col_name`
- `mysql_get`
- `mysql_is_null`

## Escaping and quoting

- `mysql_escape`
- `mysql_quote`
- `mysql_escape_id`

## Prepared statements and parameters

- `mysql_prepare`
- `mysql_params_new`
- `my_params_end`
- `mysql_bind_str`
- `mysql_bind_i32`
- `mysql_bind_null`
- `mysql_stmt_execute`
- `mysql_stmt_close`
- `mysql_stmt_reset`
- `mysql_set_param_str`
- `mysql_set_param_i32`
- `mysql_set_param_i64`
- `mysql_set_param_null`

## Transactions

- `mysql_begin`
- `mysql_commit`
- `mysql_rollback`
- `mysql_autocommit_on`
- `mysql_autocommit_off`

## Schema and discovery helpers

- `mysql_list_databases`
- `mysql_list_tables`
- `mysql_table_exists`

## Packet, buffer, and protocol helpers

- `my_to_i64`
- `my_to_i32`
- `my_buf_copy`
- `my_extract`
- `my_buf_set`
- `my_buf_get`
- `my_read_u16`
- `my_read_u32`
- `my_write_u16`
- `my_write_u24`
- `my_write_u32`
- `my_write_cstr`
- `my_read_cstr`
- `my_cstr_len`
- `my_read_lenenc_val`
- `my_lenenc_size`
- `my_read_exact`
- `mysql_read_packet`
- `mysql_write_packet`
- `my_pkt_len`
- `my_pkt_byte`
- `my_sep`
- `my_row_sep`
- `my_null_marker`
- `my_parse_ok`
- `my_parse_err`

