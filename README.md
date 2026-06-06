# AlzScript

**A programming language that reads like English. Simpler than Python. Runs on Node.js.**

```js
name = "World"
print "Hello, {name}!"
```

---

## Installation

```bash
npm install -g alzjs
```

**Requirements:** Node.js 18 or higher

---

## Quick Start

Create a file `hello.js`:

```js
name = ask "What is your name? "
print "Hello, {name}!"
```

Run it:

```bash
alz hello.js
```

---

## CLI

```
alz main.js          Run a file
alz                  Open interactive shell (REPL)
alz repl             Open interactive shell (REPL)
alz build main.js    Compile to main.compiled.mjs
alz check main.js    Check for syntax errors
alz new my-app       Scaffold a new project
alz version          Show version
alz help             Show help
```

---

## Language Reference

### Variables

No `var`, `let`, or `const`. Just assign.

```js
name = "Sarg"
age  = 23
active = true
score = 98.5
```

---

### String Interpolation

Use `{variable}` inside any string.

```js
name = "Sarg"
print "Hello, {name}!"
print "Age: {age}, Score: {score}"
```

---

### Input

```js
name = ask "Enter your name: "
print "Hello, {name}!"
```

---

### Conditions

```js
age = 20

if age >= 18:
    print "Adult"
else if age == 16:
    print "Almost there"
else:
    print "Minor"
```

Use `is` and `isnt` as readable alternatives to `==` and `!=`:

```js
if status is "active":
    print "Online"

if role isnt "admin":
    print "Access denied"
```

---

### Loops

**Repeat n times:**

```js
repeat 5 as i:
    print "Step {i}"
```

**Loop over a list:**

```js
fruits = ["apple", "mango", "grape"]
each fruit in fruits:
    print "Fruit: {fruit}"
```

**Loop over object entries:**

```js
user = { name: "Sarg", role: "admin" }
each key, val in user:
    print "{key}: {val}"
```

**Repeat until:**

```js
score = 0
repeat until score >= 100:
    score = score + 10
print "Final score: {score}"
```

---

### Functions

```js
define greet(name):
    return "Hello, {name}!"

define add(a, b):
    return a + b

print greet("Sarg")
print add(10, 20)
```

---

### Error Handling

```js
try:
    data = fetch "https://api.example.com/users"
    print data
catch err:
    print "Failed: {err}"
```

---

### Math

```js
print round(3.7)       // 4
print floor(9.9)       // 9
print ceil(1.1)        // 2
print sqrt(16)         // 4
print power(2, 10)     // 1024
print abs(-42)         // 42
print min(3, 7)        // 3
print max(3, 7)        // 7
print random()         // 0.0–1.0
```

---

### Hashing & Encoding

```js
h = hash "sha256" "hello"
print h

encoded = encode "base64" "AlzScript"
decoded = decode "base64" encoded
print decoded
```

---

### Pretty Print

Format any object or array as readable JSON:

```js
user = { name: "Sarg", age: 23, role: "admin" }
print pretty(user)
```

Output:
```json
{
  "name": "Sarg",
  "age": 23,
  "role": "admin"
}
```

---

### File System

```js
write "notes.txt" "Hello from AlzScript"
content = read "notes.txt"
print content

add to "notes.txt" "\nSecond line"

exists = file exists "notes.txt"
print exists

delete "notes.txt"
```

---

### Shell Commands

```js
result = run "echo Hello from shell"
print result

files = run "ls -la"
print files
```

---

### HTTP Requests

```js
// GET
data = fetch "https://api.example.com/users"
print pretty(data)

// POST
result = post "https://api.example.com/login" with { username: "sarg", password: "secret" }
print result.token
```

---

### Built-in Database

AlzScript includes a zero-config file-based database. No setup, no SQL, no external services.

```js
// Save a record
db.save("users", { name: "Sarg", role: "admin", age: 23 })

// Load all records
all = db.all("users")
each user in all:
    print "{user.name} | {user.role}"

// Find one record
user = db.find("users", { name: "Sarg" })
print "Found: {user.name}"

// Query with conditions
admins = db.where("users", { role: "admin" })

// Count records
total = db.count("users")
print "Total: {total}"

// First / Last
first = db.first("users")
last  = db.last("users")

// Update
db.update("users", { name: "Sarg" }, { age: 24 })

// Remove
db.remove("users", { name: "Sarg" })

// Clear all records (keep table)
db.clear("users")

// Drop table entirely
db.drop("users")
```

Records are automatically assigned a unique `_id` and a timestamp `_at`.

Data is stored in a local `.alzdata/` directory as JSON files.

---

### MySQL

```js
db.mysql.connect({
    host: "localhost",
    user: "root",
    password: "secret",
    database: "myapp"
})

rows = db.mysql.query("SELECT * FROM users WHERE active = 1")
each row in rows:
    print "{row.name} | {row.email}"

db.mysql.close()
```

---

### HTML Templates

AlzScript includes a built-in template engine for rendering HTML.

**Template file — `views/index.html`:**

```html
<!DOCTYPE html>
<html>
<head>
  <title>
show title
  </title>
</head>
<body>
  <h1>Welcome,
show user.name
  </h1>

  <ul>
  each product in products
    <li>
show product.name
    </li>
  end
  </ul>

  if user.role == "admin"
    <p><strong>Admin Panel</strong></p>
  end

  -- this is a comment, it will not appear in output --

</body>
</html>
```

**AlzScript file:**

```js
data = {
    title: "My Store",
    user: { name: "Sarg", role: "admin" },
    products: [
        { name: "AlzScript Book" },
        { name: "ALZ T-Shirt" }
    ]
}

html = render "views/index.html" with data
print html
```

**Template syntax:**

| Syntax | Description |
|---|---|
| `show variable` | Output a variable (HTML-escaped) |
| `show! variable` | Output raw/unescaped HTML |
| `show expr + 1` | Output an expression |
| `if condition` / `end` | Conditional block |
| `each item in list` / `end` | Loop block |
| `include "file.html"` | Include a partial |
| `extends "layout.html"` | Use a layout |
| `block name` / `endblock` | Named content block |
| `-- comment --` | Comment (stripped from output) |

---

### Web Server

```js
serve on 3000:
    route "/":
        respond "Hello, World!"

    route "/user/:id":
        id = request.params.id
        user = db.find("users", { _id: id })
        if user is null:
            respond 404 "User not found"
        respond pretty(user)

    route "/login" method="POST":
        body = request.body
        user = db.find("users", { name: body.name })
        if user is null:
            respond 401 "Invalid credentials"
        respond { token: "abc123", user: user.name }
```

---

## Project Structure

Use `alz new` to scaffold a new project:

```bash
alz new my-app
cd my-app
alz main.js
```

Generated structure:

```
my-app/
├── main.js        ← entry point
├── views/         ← HTML templates
├── public/        ← static files
├── .alzdata/      ← local database (auto-created)
└── package.json
```

---

## What's New in v1.0.2

- **ESM fix** — resolved `_alzCR` and `_alzdb` duplicate declaration crash on Node.js v20+
- **`.js` as primary extension** — AlzScript files use `.js`, no `.alz` extension
- **`render` as expression** — `html = render "view.html" with data` now works in assignments
- **REPL variable persistence** — variables defined in one REPL line are available in subsequent lines
- **Template engine** — `render`, `show`, `each`, `if`, `include`, `extends`, `block`
- **Database expanded** — added `db.where()`, `db.count()`, `db.first()`, `db.last()`, `db.clear()`, `db.drop()`
- **MySQL support** — `db.mysql.connect()`, `db.mysql.query()`, `db.mysql.close()`
- **New built-ins** — `hash`, `encode`, `decode`, `run`, `pretty()`

---

## License

MIT — © ALZ TECH
