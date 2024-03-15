# Tracing MySQL Optimizations

After connection to a MySQL database, we need to enable tracing:

```sql
  SET SESSION OPTIMIZER_TRACE="enabled=on"; 
```

Once that is done we can execute a statement (e.g. SELECT, EXPLAIN SELECT, UPDATE, etc.) and retrieve the tracing information from the respective table:

```sql
  <statement to trace>;
  SELECT * FROM information_schema.OPTIMIZER_TRACE;
```

The JSON output of the tracing can then be copied into a separate file on which we'll execute [opttrace](https://github.com/ogrovlen/opttrace) to get additional information.

```shell
  git clone https://github.com/ogrovlen/opttrace.git
  cd opttrace
  node joinopttrace.js path_to_tracefile.json
```

We can repeat the process for other statements: retrieving the JSON output and then executing opttrace on top of that. Once we are finished, we can go back to the MySQL database connection and stop tracing:

```sql
  SET SESSION OPTIMIZER_TRACE="enabled=off"; # disable tracing
```

## References
- https://dev.mysql.com/doc/dev/mysql-server/latest/PAGE_OPT_TRACE.html
- https://github.com/ogrovlen/opttrace
