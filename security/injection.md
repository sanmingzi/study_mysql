# injection

## simple demo of injection

```m
user_id = get_request_string("user_id");
sql = "SELECT * FROM users WHERE user_id = " + user_id;

If user_id = "1; DROP TABLE users;",
sql = SELECT * FROM users WHERE user_id = 1; DROP TABLE users;
this sql will delete all record in users, so the sql injection is very dangerous.
```
