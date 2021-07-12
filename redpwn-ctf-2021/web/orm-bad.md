Let's take a look at the `app.js` file given in the challenge.  Our first observation is that the username is 'admin', and the password is randomly generated.  We then find this statement:

```
"SELECT * FROM users WHERE username='" + req.body.username + "' AND password='" + req.body.password + "'"
```

This statement is vulnerable to SQL injection.  We will use the comment exploit to solve this challenge.  if we type in `admin'--` into the username field, the statement will look something like this:

```
SELECT * FROM users where username='admin'-- AND password='...'
```

-- is a comment in SQLite, so the part of the query after the -- is treated as a comment.  This will select a user with username `admin`, which we know exists.  Thus, we will be able to bypass the form.

We type in `admin'--` into the username field and we get the flag!

Flag: `flag{sqli_overused_again_0b4f6}`
