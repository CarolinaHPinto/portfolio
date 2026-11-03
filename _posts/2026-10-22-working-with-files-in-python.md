---
title: "Working with Files in Python: Reading Logs Like a Security Analyst"
date: 2026-10-22
categories: [Python]
tags: [python, files, parsing, log analysis]
excerpt: "Opening, reading, writing and parsing files, then building a script that flags accounts with repeated failed logins."
---

In the last post, we wrote scripts that checked logins, but we typed our data directly into the code. Real security data doesn't work that way. It lives in files, mostly **logs**, which are records of events that happen on an organization's systems. A log might hold login attempts, software update records, or errors from applications that someone is attacking.

Reading those files with Python is what turns your scripts from practice exercises into real tools. By the end of this post, you'll build a program that spots suspicious login attempts from a log file.

## Opening a file

Here's the standard way to open a file for reading:

```python
with open("update_log.txt", "r") as file:
    updates = file.read()
print(updates)
```

There's a lot packed into that first line, so let's take it apart.

**`with`** handles errors and manages outside resources for you. In this case, it automatically closes the file when you leave the indented block. You can use `open()` without `with`, but then you have to remember to close the file yourself.

**`open()`** opens the file. It takes two inputs:

1. **The file name** (as a string, in quotes), including the extension like `.txt`. If the file sits in the same folder as your Python file, the name alone is enough. If it lives somewhere else, you need the full file path starting from the root, like `"/home/analyst/logs/access_log.txt"`.
2. **The mode**, which says what you want to do:

| Mode | Meaning |
|---|---|
| `"r"` | Read the file |
| `"w"` | Write to the file, replacing everything in it (or create a new file) |
| `"a"` | Append to the end, keeping what's already there |

**`as file`** gives the open file a variable name so you can use it inside the indented block. You can call it anything, but `file` is a common choice.

Don't forget the colon at the end of the line.

## Reading a file

Inside the block, `.read()` converts the file's contents into a string:

```python
with open("update_log.txt", "r") as file:
    updates = file.read()
```

Once it's a string stored in `updates`, you can do everything you already know: `len()`, `.index()`, slicing, and so on.

## Writing to a file

Analysts write files too, for example to create an allow list of approved usernames. Use `"w"` or `"a"` along with the `.write()` method:

```python
line = "jrafael,192.168.243.140,4:56:27,True"
with open("access_log.txt", "a") as file:
    file.write(line)
```

Because the mode is `"a"`, this adds the line to the end of `access_log.txt` and leaves the existing records alone. With `"w"`, the old contents would be wiped out first, so choose carefully.

## Parsing: making data usable

Raw file contents are usually one big string, which isn't very convenient. **Parsing** means converting data into a more readable or more usable format. Two methods do most of the heavy lifting.

**`.split()`: string to list**
It breaks a string into a list at a character you choose:

```python
approved_users = "elarson,bmoreno,tshah,sgilmore,eraab"
print(approved_users.split(","))
# ['elarson', 'bmoreno', 'tshah', 'sgilmore', 'eraab']
```

If you pass nothing in, it splits at any whitespace (spaces, new lines, and so on):

```python
removed_users = "wjaffrey jsoto abernard jhill awilliam"
print(removed_users.split())
# ['wjaffrey', 'jsoto', 'abernard', 'jhill', 'awilliam']
```

**`.join()`: list to string**
This goes the other way, and its syntax looks backwards at first. You attach `.join()` to the separator and pass the list in:

```python
approved_users = ["elarson", "bmoreno", "tshah", "sgilmore", "eraab"]
print(",".join(approved_users))
# elarson,bmoreno,tshah,sgilmore,eraab
```

You'll need `.join()` before writing, since `.write()` only accepts strings. Using `"\n"` as the separator puts each element on its own line.

A typical read-modify-write flow looks like this:

```python
with open("update_log.txt", "r") as file:
    updates = file.read()
updates = updates.split()       # work with it as a list...
# ...make your changes here...
updates = " ".join(updates)     # ...then turn it back into a string
with open("update_log.txt", "w") as file:
    file.write(updates)
```

Notice that the `.split()` line is *not* indented under the first `with`. The file closes as soon as we've read it, which keeps the code tidy.

## Putting it together: detecting suspicious logins

Now for the main event. Our goal is to flag any user with **three or more failed login attempts**.

Suppose we have a text file called `failed_login_log.txt` where each entry is a username from one failed attempt:

```
tshah elarson tshah bmoreno tshah
```

### Step 1: Plan the algorithm

Break the problem into small steps:

1. Import the log file, split its contents, and store the usernames in a list called `usernames`.
2. Loop through that list. For each element, check if it matches the user we're investigating (`current_user`).
3. Each time it matches, add 1 to a counter.
4. If the counter reaches three or more, raise an alert. Otherwise, the user is fine.

### Step 2: Import the data

```python
with open("failed_login_log.txt", "r") as file:
    usernames = file.read()
usernames = usernames.split()
```

### Step 3: Wrap the logic in a function

We'll define a function called `login_check()` that takes the list of failed attempts and the user to check:

```python
def login_check(login_list, current_user):
    failed_attempts = 0
    for username in login_list:
        if username == current_user:
            failed_attempts += 1
    if failed_attempts >= 3:
        return "ALERT: " + current_user + "'s account is locked."
    else:
        return current_user + " can log in."
```

### Step 4: Run it

```python
print(login_check(usernames, "tshah"))     # ALERT: tshah's account is locked.
print(login_check(usernames, "elarson"))   # elarson can log in.
```

Look at how many pieces you've used: a variable (the counter), a `for` loop to visit every entry, an `if` statement to match users, a second `if-else` to make the decision, a function so it's reusable for any user, and file handling with `.split()` to get the data in. This is exactly the kind of script analysts write to review huge logs in seconds.

## Key takeaways

- Logs are records of system events, and most security data starts in files like these.
- Open files with `with open("filename", "mode") as file:`. The `with` keyword manages resources and closes the file for you.
- Modes: `"r"` reads, `"w"` writes (and overwrites), and `"a"` appends.
- `.read()` converts file contents to a string, and `.write()` writes a string to a file.
- Parsing makes data usable: `.split()` turns a string into a list, and `.join()` turns a list back into a string.
- Combining file handling with loops, conditionals, and functions lets you automate real investigations, like flagging accounts with repeated failed logins.

Next time you face a mountain of log data, you'll know how to let Python do the reading for you.
