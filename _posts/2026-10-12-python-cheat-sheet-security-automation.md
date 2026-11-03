---
title: "Python Cheat Sheet: Security Automation"
date: 2026-10-12
categories: [Python]
tags: [python, cheatsheet, automation, regex, debugging]
excerpt: "Everything from Course 7 of the Google Cybersecurity Certificate in one place: conditionals, loops, functions, regex, files, parsing and debugging."
---

*Google Cybersecurity Certificate, Course 7. Built from the Course 7 reference guide plus the labs and practice questions.*

## 1. Why automate security tasks

- **Saves time:** the computer does repetitive jobs, like checking logs.
- **Fewer mistakes:** a program runs the same steps the same way every time.
- **Faster response:** it can spot problems, like many failed logins, right away.
- **More time for hard work:** people can focus on complex problems.

Suspicious activity Python can track:

- Several failed login attempts in a short time
- Logins from IP addresses outside established work zones
- Logins outside normal work hours

Python cannot track phishing that happens through in-person interactions.

## 2. Comments

```python
# Single-line comment
"""
Multi-line comment / docstring.
Use when you need more than 79 characters.
"""
```

## 3. Conditional statements

```python
if device_id != "la858zn":
    print("unknown device")
elif status == 500:
    print("server error")
else:
    print("ok")
```

- `if` starts the check. `elif` runs only if earlier conditions were False. `else` runs only if all earlier conditions were False.
- The keyword is `elif`, not `elsif`.
- Every `if`, `elif`, `else`, `for`, `while` and `def` line ends with a colon, and the code inside is indented.

**Logical operators**

```python
if username == "bmoreno" and login_attempts < 5:   # both must be True
if status == 100 or status == 102:                 # at least one True
if not account_status == "removed":                # flips True/False
if user in approved_list:                          # membership check
```

Comparison operators: `==` equal, `!=` not equal, `<` `>` `<=` `>=`

`=` assigns a value. `==` compares two values.

## 4. Loops (iterative statements)

```python
# for loop: go through a sequence
for username in ["bmoreno", "tshah", "elarson"]:
    print(username)

for i in range(10):   # i = 0, 1, ... 9
    print(i)

# while loop: repeat while a condition is True
while login_attempts < 5:
    login_attempts = login_attempts + 1
```

- **for loop:** does the same action a set number of times, based on a sequence (a list of IP addresses, log entries, and so on).
- **while loop:** repeats based on a condition. Something inside must change the condition, or it never ends.
- `break` exits the loop completely. `continue` skips to the next iteration.
- `range(start, stop, step)`: start is included, stop is excluded. Defaults are start = 0 and step = 1, so `range(5)` gives 0 to 4.

## 5. Counter pattern (loop + conditional + counter)

Example: count systems that need updates.

```python
systems = ["OS 1", "OS 2", "OS 3", "OS 4"]
needs_update = ["OS 2", "OS 4"]
count = 0

for system in systems:
    if system in needs_update:
        print(system, "needs an update")
        count = count + 1

print("Total systems needing updates:", count)
```

- The loop checks every item.
- The `if` decides whether the item matches.
- The counter adds 1 each time it does.

## 6. User-defined functions

```python
def greet_employee():
    print("Welcome")

def calculate_fails(total_attempts, failed_attempts):
    fail_percentage = failed_attempts / total_attempts
    return fail_percentage   # exits the function and sends back a value

result = calculate_fails(100, 20)
```

- `def` defines a function. Names inside the parentheses are parameters.
- Define a function before you call it.
- `return` sends a value back and ends the function.
- Benefit of a function: you write the steps once and reuse them with different inputs.

## 7. Built-in functions

| Function | What it does | Example |
|---|---|---|
| `print()` | Outputs to the screen | `print("login success")` |
| `type()` | Returns the data type | `type(51.1)` gives `float` |
| `range()` | Generates a sequence of numbers | `range(0, 5, 1)` gives 0,1,2,3,4 |
| `max()` | Largest value | `max(10, 15, 5)` gives 15 |
| `min()` | Smallest value | `min(10, 15, 5)` gives 5 |
| `sorted()` | Sorts a list (smallest to largest, or A to Z) | `sorted([10, 15, 5])` gives `[5, 10, 15]` |
| `str()` | Converts to a string | `str(10)` gives `"10"` |
| `len()` | Number of elements or characters | `len("security")` gives 8 |

## 8. Importing modules and libraries

```python
import statistics                      # whole module
from statistics import mean            # one function
from statistics import mean, median
```

## 9. String methods

```python
"Security".upper()      # "SECURITY"
"Security".lower()      # "security"
"Security".index("c")   # 2 (first occurrence)
```

## 10. List methods

```python
users = ["elarson", "fgarcia", "tshah"]
users.insert(2, "wjaffrey")   # add at index 2
users.remove("elarson")       # remove first match
users.append("btang")         # add to the end
users.index("tshah")          # find index of first match
```

## 11. Working with strings and lists

```python
# Concatenation with +
device_id = "IT" + "nwp12"                                # "ITnwp12"
users = ["elarson", "bmoreno"] + ["tshah", "btang"]       # combined list

# Bracket notation (indexing and slicing)
"h32rb17"[0]          # "h" (indexes start at 0)
"h32rb17"[0:3]        # "h32" (start included, end excluded)
username_list[2]      # third element of a list
username_list[-1]     # last element of a list
```

**Index rule:** a list with 5 items has indexes 0 to 4. Using index 5 raises an `IndexError`.

## 12. Regular expressions

```python
import re
re.findall(pattern, string)   # returns a list of all matches
```

Example string: `"a53-32c .E"`

| Symbol | Matches | Result |
|---|---|---|
| `a53` | The literal text | `["a53"]` |
| `\w` | Any alphanumeric character or underscore | `["a","5","3","3","2","c","E"]` |
| `.` | Any character, including symbols | every character |
| `\d` | A single digit | `["5","3","3","2"]` |
| `\s` | A single whitespace | `[" "]` |
| `\.` | A literal period | `["."]` |
| `+` | One or more of the previous character | `\w+` gives `["a53","32c","E"]` |
| `*` | Zero or more of the previous character | `\w*` also returns empty matches |
| `{n}` | Exactly n of the previous character | `\w{3}` gives `["a53","32c"]` |

## 13. File operations

```python
# Read
with open("login_attempts.txt", "r") as file:
    file_text = file.read()   # whole file as one string

# Write (overwrites existing content)
with open("update_log.txt", "w") as file:
    file.write("new content")

# Append (adds to the end)
with open("access_log.txt", "a") as file:
    file.write("jrafael")
```

| Mode | Meaning |
|---|---|
| `"r"` | Read |
| `"w"` | Write (replaces contents, or creates the file if it doesn't exist) |
| `"a"` | Append (adds to the end) |

**What `with open("ip_addresses.txt", "r") as file:` does**

- Opens the file in read mode (it does not create it or write to it).
- Stores the file object in the variable `file` while inside the `with` block.
- Closes the file automatically when the block ends, even if an error happens.

**Other file notes**

- Syntax is `open(filename, mode)`. The filename comes first.
- `.read()` is called on the file object and returns a string.
- `.write()` writes a string to the file.
- Common security log formats: `.txt` and `.csv`. (Not `.jpeg` or `.gif`.)
- Security information is often found in log files, so file skills matter for automation.
- `.write()` adds no new line by itself. If an appended entry runs into the last line, use `file.write("\n" + entry)`.

## 14. Parsing

Parsing means converting data into a format that is easier to read and work with, such as turning a string into a list.

```python
# split(): string to list
"wjaffrey jsoto abernard".split()          # splits on whitespace
"elarson,bmoreno,tshah".split(",")         # splits on a comma (the delimiter)

# join(): list to string
",".join(["elarson", "bmoreno", "tshah"])  # "elarson,bmoreno,tshah"
"\n".join(ip_list)                         # one item per line
```

**Splitting a log entry**

```python
log_entry = "jrafael,192.168.243.140,4:56:27,2022-05-09"
pieces = log_entry.split(",")
# ['jrafael', '192.168.243.140', '4:56:27', '2022-05-09']
pieces[1]   # the IP address
```

- For a whole log file, split the text into lines first, then split each line by commas.
- `.split()` and `.join()` are string methods. Call them on a string: `ip_addresses.split()`, not `split.ip_addresses()`.

## 15. Workflow: read a log, parse it, filter it

```python
with open("logs.txt", "r") as file:
    log_text = file.read()

logins = log_text.split()        # string to list
failed_logins = []

for login in logins:             # loop through each item
    if "failed" in login:        # check a condition
        failed_logins.append(login)
```

This pattern uses a `for` loop, an `if` statement and `.split()`. Add a counter only if the task asks you to count.

## 16. Algorithm: update an allow list

Goal: remove IP addresses on a remove list from a file of allowed IP addresses.

```python
import_file = "allow_list.txt"
remove_list = ["192.168.97.225", "192.168.158.170"]

# 1. Read the file into a string
with open(import_file, "r") as file:
    ip_addresses = file.read()

# 2. Convert the string to a list
ip_addresses = ip_addresses.split()

# 3. Loop through the remove list
for element in remove_list:
    # 4. Only remove if it is in the allow list
    if element in ip_addresses:
        ip_addresses.remove(element)

# 5. Convert the list back to a string
ip_addresses = "\n".join(ip_addresses)

# 6. Write the result over the original file
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

**Same algorithm as a reusable function**

```python
def update_file(import_file, remove_list):
    with open(import_file, "r") as file:
        ip_addresses = file.read()
    ip_addresses = ip_addresses.split()
    for element in remove_list:
        if element in ip_addresses:
            ip_addresses.remove(element)
    ip_addresses = " ".join(ip_addresses)
    with open(import_file, "w") as file:
        file.write(ip_addresses)

update_file("allow_list.txt", ["192.168.25.60", "192.168.140.81"])
```

**Why each step**

- `.read()` gets the file text so Python can work with it.
- `.split()` makes a list so each IP address can be removed on its own.
- The `for` loop checks each address on the remove list.
- The `if element in ip_addresses` check prevents an error, because `.remove()` fails if the item is not in the list.
- Using `.remove()` this way works because there are no duplicates in the list.
- `.join()` turns the list back into a string, which `.write()` needs.
- Mode `"w"` replaces the old file contents with the updated list.

**Creating a new file:** open it with `"w"` and write a string to it.

```python
with open("allow_list.txt", "w") as file:
    file.write(ip_addresses)
```

*See this algorithm in my [IP allow list project]({{ '/projects/python-allow-list/' | relative_url }}).*

## 17. Debugging

Debugging is the practice of identifying and fixing errors in code.

**Types of errors**

| Error type | What it is | Example |
|---|---|---|
| Syntax error | Breaks Python's rules, so the code won't run | Missing colon, missing quote or comma, unbalanced parentheses, `=` instead of `==`, `elsif` instead of `elif` |
| Exception | An error that happens while the code runs | `IndexError`, `NameError`, `IndentationError` |
| Logic error | Code runs but gives the wrong result, with no error message | Wrong list index, missing `else`, wrong operator |

**Common exceptions**

- `NameError`: using a variable or function that doesn't exist, often a typo (`username_list` instead of `usernames_list`).
- `IndexError`: list index out of range (`usernames_list[5]` on a 5-item list).
- `IndentationError`: code that should be indented under `if`, `for`, `with` or `def` is not.
- `SyntaxError: unexpected EOF while parsing`: the code ends early, such as a `with` or `for` line with no body, or an unclosed parenthesis.

**Debugging tips**

- Read the error message. It gives the error type and the line number.
- Fix one error at a time, and run the code after each fix. Some errors only appear after the earlier ones are fixed.
- Logic errors give no warning. Test different input values and check the output.
- Place `print()` statements in and around a function to see values at each step.

**Fixes from the lab**

```python
for i in range(10):                                  # add the missing colon
    print("Connection cannot be established")

usernames = ["tbailey", "zdutchma", "esmith"]        # close the quote, add the comma

print("update needed".upper())                       # close the parenthesis

for name in usernames_list:                          # spell the variable correctly
    if name == username:                             # == to compare
        print("The user is an approved user")        # indent under the if

if username == usernames_list[4]:                    # last of 5 items (or use [-1])

with open(import_file, "r") as file:                 # add the colon
ip_addresses = ip_addresses.split()                  # call split on the string

# Logic error: match each OS to the right index
if system == "OS 1":
    print("Patch date:", patch_schedule[0])
elif system == "OS 2":
    print("Patch date:", patch_schedule[1])
elif system == "OS 3":
    print("Patch date:", patch_schedule[2])
```

**Missing else example**

```python
def check_user(name):
    if name == "jhill":
        print("user flagged")
    else:
        print("user okay")
```

## 18. Common mistakes checklist

- Forgetting the colon after `if`, `elif`, `else`, `for`, `while`, `def` and `with`.
- Mixing up `=` (assign) and `==` (compare).
- Typing `elsif` instead of `elif`.
- Off-by-one errors: indexes start at 0, and slice and `range()` end values are excluded.
- Calling a function before it is defined.
- Using `open("r", "logs.txt")`. The filename goes first, then the mode.
- Forgetting that `.split()` with no argument splits on whitespace.
- Using `"w"` when you meant `"a"`. Write mode erases the existing contents.
- Forgetting to convert a list back to a string with `.join()` before `.write()`.

## 19. Quick answers

- Types of errors while debugging: syntax errors, logic errors, exceptions.
- Program sends data to the wrong place but runs fine: logic error.
- Error message about an unknown index: exception (`IndexError`).
- Same action a set number of times over a sequence: `for` loop.
- Log file formats: `.txt`, `.csv`.
- String to list: `.split()`. List to string: `.join()`.
- Read / append / write: `"r"` / `"a"` / `"w"`.
