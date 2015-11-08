# Playing with Play Framework database rollback strategy 

I was trying to figure out how Play handles database rollbacks using evolutions and I don't think there is a better
way than getting hands dirty. 

This is very simple Play Framework project that contains only database configuration and database evolutions that 
are applied to the database on a start up. As soon as the app is running you can stop it as db changes has been
 applied and there is nothing else it will do.

To simulate rollback I need at least 2 versions and each creating a table in db. 1st one is on branch `rback-ev1` and 
2nd on `rback-ev2`.   

Steps:
 1. checkout `rback-ev1`
 2. run it `activator clean start` - this should create 'people' table
 3. stop it and check that tables has been created, see [List tables in the database](#list-tables-in-the-database)
 4. checkout `rback-ev2`
 5. run it `activator clean start` - this should create 'company' table
 6. stop it and check that tables has been created, see [List tables in the database](#list-tables-in-the-database)
 7. checkout `rback-ev1`
 8. run it `activator clean start` - this should rollback 'company' table
 9. stop it and check that tables has been created, see [List tables in the database](#list-tables-in-the-database)

### List tables in the database

```
java -cp ~/.ivy2/cache/com.h2database/h2/jars/h2-1.4.187.jar  org.h2.tools.Shell -sql "show tables" -url "jdbc:h2:~/tmp/h2db/test-rollback"
```