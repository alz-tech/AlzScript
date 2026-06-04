AlzScript — A beginner-friendly programming language that reads like English. Transpiles to JavaScript. Runs on Node.js.

> Write plain English. Runs on Node.js.

---

## Install

```bash
npm install -g alzjs
```

The command you use is just `alz`.

```bash
alz version
```

That's it. You're ready.

---

## Run a file

```bash
alz myapp.alz
```

Or with the explicit keyword:

```bash
alz run myapp.alz
```

---

## Interactive shell

```bash
alz
```

Opens the ALZ shell where you can type code line by line.

```
alz › name = "Sara"
alz › print "Hello {name}"
Hello Sara
alz › exit
```

---

## Other commands

```bash
alz build myapp.alz    # compile to myapp.js
alz check myapp.alz    # check for errors without runningalz version            # show version
alz help               # show help
```

---

## The language

### Variables

```alz
name   = "Sara"
age    = 25
price  = 9.99
active = true
empty  = null
```

### Output

```alz
print "Hello"
print "Hello {name}"
print "Name: {name}, Age: {age}"
print
```

### Input

```alz
name = ask "What is your name? "
print "Hello {name}"
```

### Conditions

```alz
if age > 18:
    print "Adult"
else if age == 18:
    print "Just 18"
else:
    print "Minor"
```

```alz
if name is "Sara":
    print "Found her"

if name isnt "Bob":
    print "Not Bob"
```

### Loops

```alz
repeat 5:
    print "Hello"

repeat 5 as i:
    print "Step {i}"

each item in items:
    print item

repeat until score > 100:
    score = score + 10
```

### Functions

```alz
define greet(name):
    print "Hello {name}"

define add(a, b):
    return a + b

greet("World")
result = add(10, 5)
print result
```

### Lists

```alz
fruits = ["apple", "mango", "banana"]
fruits.add("grape")
fruits.remove("mango")
fruits.sort()
print fruits.length
print fruits.has("apple")
```

### Objects

```alz
user = { name: "Sara", age: 25 }
print user.name
user.age = 26
```

### Math

```alz
x = round(3.7)
x = floor(9.9)
x = sqrt(16)
x = abs(-5)
x = max(3, 7)
x = min(3, 7)
x = power(2, 8)
x = random()
```

### Files

```alz
content = read "notes.txt"
write "notes.txt" "Hello World"
add to "notes.txt" "New line"
delete "notes.txt"
exists = file exists "notes.txt"
```

### HTTP

```alz
data = fetch "https://api.example.com/users"
print data
```

### Web server

```alz
serve on 3000:
    route "/":
        respond "Hello World"

    route "/greet" method="POST":
        name = request.name
        respond "Hello {name}"
```

### Database

No SQL. No setup. Just works.

```alz
db.save("users", { name: "Sara", age: 25 })
all    = db.all("users")
one    = db.find("users", { name: "Sara" })
db.update("users", { name: "Sara" }, { age: 26 })
db.remove("users", { name: "Sara" })
```

Data is stored in `.alzdata/` folder as JSON files.

### Error handling

```alz
try:
    data = fetch "https://api.example.com"
    print data
catch err:
    print "Failed: {err}"
```

### Comments

```alz
// single line
# single line
/* multi
   line */
```

---

## How it works

```
your .alz file
      ↓
   Lexer        reads your code, produces tokens
      ↓
   Parser       turns tokens into a tree (AST)
      ↓
   Codegen      converts the tree to JavaScript
      ↓
   Node.js      runs the JavaScript
```

You never see the JavaScript. You just write ALZ.

---

## License

MIT — ALZ TECH
