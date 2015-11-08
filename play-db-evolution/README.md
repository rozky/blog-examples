# Playing with Play Framework rollback strategy 

List existing tables in the database

```
java -cp ~/.ivy2/cache/com.h2database/h2/jars/h2-1.4.187.jar  org.h2.tools.Shell -sql "show tables" -url "jdbc:h2:~/tmp/h2db/test-rollback"
```