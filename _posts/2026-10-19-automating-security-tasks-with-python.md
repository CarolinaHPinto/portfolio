---
title: "Automating Security Tasks with Python: Putting It All Together"
date: 2026-10-19
categories: [Python]
tags: [python, automation, devsecops, log analysis]
excerpt: "Login timeouts, suspicious-login tracking and failed-password monitoring: three security scripts built from the basics."
---

Over this series, we've collected a pile of tools: strings, lists, and regular expressions. Now it's time to build something with them. Think of it like moving from collecting LEGO bricks to assembling a working model. The model we're building today is **automation**.

Automation means using technology to cut down the manual effort of common, repetitive tasks. For a security analyst, that's most of Python's value. Nobody wants to read through thousands of login records by hand, and humans get tired and miss things. A script doesn't.

## The building blocks

Every automation script you write will lean on the same handful of components:

| Component | What it does for automation |
|---|---|
| Variables | Store data once so you don't retype values for every action |
| Conditional statements | Check whether something meets a condition before acting on it |
| Iterative statements (`for`, `while`) | Repeat the same steps without retyping code. A `for` loop repeats over a sequence, a `while` loop repeats while a condition holds |
| Functions | Package code you can define once and reuse anywhere |
| Strings and lists | Hold and slice up the data you'll work with: usernames, IPs, log lines |
| Files | Where your security data usually starts out (more on this below) |

Let's see them work together in three real security scenarios.

## Example 1: Enforcing a login timeout

Imagine a database that should lock a user out if they take too long to log in after typing their username. That slows down attackers who are guessing passwords. Python can track how long it takes from the moment a username is entered until the correct password is provided, then compare that to a time limit.

```python
TIMEOUT_SECONDS = 30

def check_login_time(username_entered_at, password_correct_at):
    elapsed = password_correct_at - username_entered_at
    if elapsed > TIMEOUT_SECONDS:
        return "Locked out: login took too long"
    return "Login allowed"

# Timestamps in seconds
print(check_login_time(100, 112))   # Login allowed
print(check_login_time(100, 160))   # Locked out: login took too long
```

Here a variable holds the limit, a function packages the check, and a conditional makes the decision. (In a real system, you'd get the timestamps from Python's `time` module instead of typing them in.)

## Example 2: Tracking user logins

Next, suppose you want to review each login for warning signs: odd hours, unapproved locations, or the same account logging in from multiple IP addresses at once. Python can check the timestamps, IP addresses, and locations attached to each login and flag anything suspicious.

Here's a simplified version that checks the hour of day and the location:

```python
approved_locations = ["Miami", "Chicago"]

logins = [
    ["bmoreno", 9, "Miami"],
    ["tshah", 3, "Lagos"],
    ["sgilmore", 14, "Chicago"],
]

for username, hour, location in logins:
    if hour < 6 or hour > 20:
        print("Flag:", username, "logged in at an unusual hour")
    if location not in approved_locations:
        print("Flag:", username, "logged in from an unapproved location")
```

Output:

```
Flag: tshah logged in at an unusual hour
Flag: tshah logged in from an unapproved location
```

The list holds the data, the loop visits every login, and the conditionals decide what's worth flagging. Notice that `for username, hour, location in logins` unpacks each small list into three variables, which keeps the code readable.

## Example 3: Monitoring failed password attempts

Many failed logins in a short period is a classic sign of password guessing. This data usually lives in log files, so Python needs to **parse** each line, meaning pull out the useful pieces like the username, IP address, timestamp, and login status.

First, a reusable counting function. This is the "count the logins for a flagged user" pattern: a `for` loop, a conditional, and a counter variable.

```python
def count_occurrences(target, items):
    count = 0
    for item in items:
        if item == target:
            count += 1
    return count
```

Now we can parse some log lines. Each line holds comma-separated values, and the string method `.split(",")` breaks a line into a list of pieces:

```python
log_lines = [
    "tshah,192.168.1.10,2026-10-19 09:15:02,FAILED",
    "tshah,192.168.1.10,2026-10-19 09:15:09,FAILED",
    "bmoreno,10.0.0.5,2026-10-19 09:15:30,FAILED",
    "tshah,192.168.1.10,2026-10-19 09:15:14,FAILED",
    "sgilmore,172.16.0.8,2026-10-19 09:16:01,SUCCESS",
]

failed_users = []
for line in log_lines:
    username, ip, timestamp, status = line.split(",")
    if status == "FAILED":
        failed_users.append(username)

flagged = []
for user in failed_users:
    if count_occurrences(user, failed_users) >= 3 and user not in flagged:
        flagged.append(user)

print(flagged)   # ['tshah']
```

Strings, lists, loops, conditionals, and a function all showed up in one small script. This version simply counts failures, but a production version would also compare the timestamps to catch attempts bunched into a short window.

## A note on files

In real work, you won't type log lines into your script. Security data typically starts in **log files**, which are records of events on a system, with new lines added as time passes. The two most common formats are:

- **.txt files:** plain text with no required structure (values might be separated by spaces or anything else)
- **.csv files:** "comma-separated values," where each value on a line is separated by a comma

Both are plain text, with no fonts, colors, or images, which makes them easy for Python to read, extract data from, and convert. Reading and writing files is the next skill to learn.

## Bonus: automation inside the software pipeline

Automation isn't just for analyzing logs. Teams also build Python security checks directly into their **CI/CD pipelines**, the automated processes that build, test, and release software. This approach is called **DevSecOps** (Development, Security, and Operations working together), and the idea is that security is built in from the start instead of bolted on at the end.

Python scripts can run inside tools like Jenkins, GitLab CI, and CircleCI to handle jobs such as:

- Running code and dependency scans, then stopping a release if serious problems appear
- Scanning for passwords and keys accidentally written into code
- Checking that releases follow security policies and compliance rules

The benefits are the same as everywhere else in automation: checks run faster, consistently every time, and early, when problems are cheapest to fix. It also frees security teams from repetitive work so they can focus on bigger problems.

## Key takeaways

- Automation reduces manual effort on repetitive tasks, and it's one of the main reasons analysts use Python.
- The core components are variables, conditionals, loops, functions, and techniques for working with strings and lists.
- Python can enforce login timeouts, track suspicious logins (odd hours, unapproved locations, multiple IPs), and monitor failed password attempts by parsing logs.
- Security data usually starts in `.txt` or `.csv` log files, so file handling is the next essential skill.
- Python also powers DevSecOps, building security checks right into CI/CD pipelines.

You now have the pieces to start writing real security scripts. Next up: opening, reading, and writing files so your code can work with actual logs.
