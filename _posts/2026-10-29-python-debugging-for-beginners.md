---
title: "Debugging in Python: How to Find and Fix Your Mistakes"
date: 2026-10-29
categories: [Python]
tags: [python, debugging, beginners]
excerpt: "Syntax errors, logic errors and exceptions, plus print statements, debuggers and a word on AI coding assistants."
---

Every programmer writes code that doesn't work the first time. Security analysts are no exception. Getting an error message isn't a sign you're doing something wrong. It's a normal part of the job, and the real skill is knowing how to track down the problem and fix it.

Think of debugging as being a detective. Every error leaves clues, and once you know what kind of error you're dealing with, you know where to look.

## The three types of errors

### 1. Syntax errors: breaking the grammar rules

A **syntax error** means you used the Python language incorrectly. Common culprits are a forgotten colon after a function header, a missing closing bracket on a list, or a quotation mark that never closes.

```python
message = "You are debugging a syntax error
print(message)
```

Python refuses to run this and points to the exact line and part of the code where it got confused. Syntax errors are labeled `SyntaxError`, followed by a description (the wording varies a bit between Python versions, such as "unterminated string literal" or "invalid syntax"). The fix here is to add the missing quotation mark.

You may also see an `IndentationError`, which is a special kind of syntax error that happens when a line's indentation is wrong.

The good news is that syntax errors are usually the easiest to fix, because the message tells you where to look.

### 2. Logic errors: the code runs, but the answer is wrong

A **logic error** happens when your code is valid but doesn't do what you intended. There's no error message, because as far as Python is concerned, nothing is wrong. That makes these the sneakiest bugs.

A classic cause is using the wrong operator, like `>=` when you meant `<`:

```python
login_attempts = 5
if login_attempts >= 5:
    print("User has not reached maximum number of login attempts.")
else:
    print("User has reached maximum number of login attempts.")
```

With five attempts used, this prints that the user has *not* reached the maximum, which is the opposite of the truth. The condition should have been `login_attempts < 5`. Similarly, using `<` when you needed `<=` can quietly leave out a value you needed.

Logic errors can also come from assigning the wrong value or from indentation that makes a line run when you didn't plan for it.

### 3. Exceptions: valid code that can't be executed

An **exception** happens when your syntax is fine but Python still can't carry out an instruction. Here are the ones you'll meet most often:

| Exception | What caused it |
|---|---|
| `NameError` | Using a variable that was never assigned, or a function that was never defined (often just a typo) |
| `IndexError` | Using an index that doesn't exist, like `usernames[3]` in a three-item list |
| `TypeError` | Using the wrong data type, like adding a string to an integer |
| `ZeroDivisionError` | Dividing by zero |
| `FileNotFoundError` | Opening a file that isn't where you said it was |

Here's a `NameError` in action:

```python
username = "elarson"
total_logins = 75
failed_logins = 18

print("Total logins:", total_logins)
print("Failed logins:", failed_logins)
print("Unusual logins:", unusual_logins)
```

The error message names `unusual_logins`, and the fix is to give that variable a value (or correct a misspelling if that's what caused it).

One more thing to know: if your code has several problems, Python reports them **one at a time**, starting with the first one it hits. Fix it, run again, and the next one appears.

## Debugging technique 1: print statements

Syntax errors and many exceptions explain themselves. Logic errors don't, so you have to investigate. The simplest tool is the humble `print()`. By dropping temporary print statements around your code, you can see exactly which parts run and in what order.

Here's a function meant to add new users to an approved list, skipping anyone already on it:

```python
new_users = ["sgilmore", "bmoreno"]
approved_users = ["bmoreno", "tshah", "elarson"]

def add_users():
    for user in new_users:
        if user in approved_users:
            print(user, "already in list")
        approved_users.append(user)

add_users()
print(approved_users)
```

The output says `bmoreno already in list`, yet the final list contains `bmoreno` twice. Something's off. Let's add print statements with descriptive labels:

```python
def add_users():
    for user in new_users:
        print("line 5 - inside for loop")
        if user in approved_users:
            print("line 7 - inside if statement")
            print(user, "already in list")
        print("line 9 - before .append method")
        approved_users.append(user)
```

Reading the output:

- "inside for loop" prints twice, once per new user. That's expected.
- "inside if statement" prints once, since only one user was already on the list. Also expected.
- "before .append method" prints twice. **That's the clue.** `.append()` runs for both users, including the one who's already approved.

The bug is isolated: `.append()` needs to be inside an `else` block so it only runs when the user is *not* already in the list:

```python
def add_users():
    for user in new_users:
        if user in approved_users:
            print(user, "already in list")
        else:
            approved_users.append(user)
```

Notice that the final version has the print statements removed. Once the bug is fixed, delete your debugging prints so your code stays clean and efficient.

### Another logic error: order matters

Sometimes the fix is simply reordering your code. Consider this function:

```python
def login_status(attempts):
    return "Account active"
    if attempts >= 5:
        return "Account locked"
```

It always returns "Account active." Once Python hits a `return` statement, the function ends immediately, so the `if` check below it never gets evaluated. Adding a print statement above the `if` would show that it never runs, which is a strong hint. The fix is to move the conditional before the return:

```python
def login_status(attempts):
    if attempts >= 5:
        return "Account locked"
    return "Account active"
```

## Debugging technique 2: debuggers

When the code gets bigger, print statements everywhere can get messy. That's where a **debugger** helps. This is a tool built into many IDEs (Integrated Development Environments, which are programs for writing code with editing and error-checking help).

Debuggers work with **breakpoints**, markers you place on specific lines. The program runs up to a breakpoint and stops, letting you test sections of your code one at a time to isolate the problem. Many debuggers also let you watch the values stored in your variables as they change, which is especially useful for catching the exact moment something goes wrong in a logic error. Debuggers help with both logic errors and exceptions.

## A word on AI coding assistants

Many IDEs now offer AI assistants that can help analyze code, spot errors, and suggest fixes. They can be a big time-saver, but their suggestions may not always be accurate, optimal, or secure. Treat them like a helpful co-pilot: review and validate anything they give you before you run it, and stay responsible for your final code.

## Key takeaways

- **Syntax errors** break Python's grammar rules. The error message usually shows you where.
- **Logic errors** run without complaint but give wrong results, so you have to investigate.
- **Exceptions** are valid code that can't be executed, like `NameError`, `IndexError`, `TypeError`, and `FileNotFoundError`.
- Python reports errors one at a time, so fix and re-run.
- **Print statements** let you trace which parts of your code run. Remove them once the bug is fixed.
- **Debuggers** and breakpoints let you pause and inspect your code piece by piece.
- Check and validate any AI-assisted suggestions before relying on them.

Bugs are inevitable, but with these techniques you'll spend a lot less time stuck on them.
