---
title: "Learning Python, Week Three: I Stopped Typing the Same Line Four Times"
date: 2026-10-01
categories: [Python]
tags: [python, loops, automation, beginners]
excerpt: "For loops, while loops, range(), break and continue, and the three mistakes I kept making."
---

```
0 I stopped typing the same line four times
1 I stopped typing the same line four times
2 I stopped typing the same line four times
3 I stopped typing the same line four times
```

Loops were the first thing in Python that made me feel like the computer was actually working for me. Here is what finally made them click.

While learning how to check login attempts without writing the same few lines four times over, I ran into **iterative statements** — most people just call them **loops**. A loop is code that runs the same set of instructions repeatedly, so you write it once and let the computer handle the repetition instead of typing it out by hand.

Depending on what you tell it, a loop might run zero times, four times, or keep going until something changes. There are two kinds you will meet first: `for` loops and `while` loops. They solve slightly different problems, and knowing which is which is most of the battle.

## For loops: when you know what you are looping through

Use a `for` loop when you already have a sequence in hand. A list of usernames, a list of assets, the characters in a word. You are saying: go through these, one at a time, and do this thing to each one.

```python
for i in ["elarson", "bmoreno", "tshah", "sgilmore"]:
    print(i)
```

What it prints:

```
elarson
bmoreno
tshah
sgilmore
```

Two lines. Four usernames. That first line is the **loop header**, and it has four parts worth naming, because being able to name them is what lets you fix your own mistakes later:

- `for` starts the loop.
- `i` is the **loop variable**. It holds one item at a time. On the first pass it is `"elarson"`, on the second it is `"bmoreno"`, and so on.
- `in` comes right before the sequence you are looping through.
- **The colon** at the end. Forget it and Python stops and complains. I forgot it constantly.

Everything underneath is the **loop body**, and it has to be indented further than the header. That indentation is not decoration. It is how Python knows which lines belong to the loop. This is the other mistake I made every day for a week.

The loop variable can be named anything. Naming it something meaningful makes the code read like a sentence:

```python
computer_assets = ["laptop1", "desktop20", "smartphone03"]
for asset in computer_assets:
    print(asset)
```

What it prints:

```
laptop1
desktop20
smartphone03
```

"For asset in computer assets, print asset." You can almost read it out loud. If you are heading toward security work, this is the shape of a lot of real tasks: you have a list of devices, or IP addresses, or employees, and you need to check each one against something.

Strings work too, which surprised me. Loop over a string and you get one character at a time:

```python
string = "security"
for character in string:
    print(character)
```

What it prints:

```
s
e
c
u
r
i
t
y
```

## When you just want to repeat something N times

Sometimes there is no list. You just want to do something ten times. That is what `range()` is for: it generates a sequence of numbers on demand. You give it a start, a stop, and how much to count by.

```python
for i in range(0, 5, 1):
    print(i)
```

What it prints:

```
0
1
2
3
4
```

Look at that output again. You asked for 0 to 5 and got 0 through 4. This is the thing that tripped me up hardest: **the start is included, the stop is not.** The loop stops one short of the number you named. It feels wrong until you have been bitten by it once, and then it never feels wrong again.

The start and the step have defaults of 0 and 1, so if that is what you want, you can leave them out. This does exactly the same thing as the version above:

```python
for i in range(5):
    print(i)
```

The stop point is the one you always have to write. If you want to start somewhere other than 0, or count by something other than 1, spell those out.

## While loops: when you do not know how many times

A `while` loop does not walk through a sequence. It keeps going as long as a condition is true, and stops the moment that condition becomes false. You use it when the number of repetitions depends on what happens.

```python
i = 1
while i < 5:
    print(i)
    i = i + 1
```

What it prints:

```
1
2
3
4
```

Notice the difference from a `for` loop. There is no loop variable in the header. You create `i` yourself on the line before, and then **you are responsible for changing it inside the loop**. That last line, `i = i + 1`, is the loop's off switch. Leave it out and `i` stays at 1 forever, the condition stays true forever, and your program never stops.

Counting is the common case. Say you want to track login attempts:

```python
login_attempts = 0
while login_attempts < 5:
    print("Login attempts:", login_attempts)
    login_attempts = login_attempts + 1
```

What it prints:

```
Login attempts: 0
Login attempts: 1
Login attempts: 2
Login attempts: 3
Login attempts: 4
```

Five lines, ending at 4. Same off-by-one feeling as `range()`, same reason: the check happens before each pass, and once the count hits 5 the condition is false and the loop is done.

The condition does not have to be a number. It can be a `True` or `False` value that something else in the loop flips:

```python
count = 0
login_status = True
while login_status == True:
    print("Try again.")
    count = count + 1
    if count == 4:
        login_status = False
```

What it prints:

```
Try again.
Try again.
Try again.
Try again.
```

This one runs an indeterminate number of times as far as the header is concerned. It keeps going until something inside decides to turn the switch off. That is the real personality of a `while` loop.

## Two words that give you an escape hatch

Once your loops are running, you will want more control than "do this to every single item." Two keywords handle almost everything, and both live inside an `if` statement in the loop body.

### `break` stops the whole loop

```python
computer_assets = ["laptop1", "desktop20", "smartphone03"]
for asset in computer_assets:
    if asset == "desktop20":
        break
    print(asset)
```

What it prints:

```
laptop1
```

The loop reaches `"desktop20"` on the second pass and walks out entirely. `"smartphone03"` never gets a turn, even though it was sitting right there in the list.

### `continue` skips one and keeps going

```python
computer_assets = ["laptop1", "desktop20", "smartphone03"]
for asset in computer_assets:
    if asset == "desktop20":
        continue
    print(asset)
```

What it prints:

```
laptop1
smartphone03
```

Same list, same condition, one word different. `"desktop20"` gets skipped, and the loop carries on to the next item. I remember it as: **`break` leaves the building, `continue` skips the meeting.**

## About the loop that never ends

You will write one. Everyone does. An **infinite loop** is a loop whose condition never becomes false, usually because you forgot to change the variable it depends on. Your program just sits there, or floods the screen, and nothing you click helps.

Press **Ctrl-C** (or Ctrl-Z) to stop it. That is it. That is the whole fix. It is not a crash and you have not broken anything.

Worth knowing: infinite loops are not always a bug. A web server or a monitoring service is often a loop that is supposed to run until someone shuts it down. The difference is whether you meant it.

## The three mistakes I kept making

- **Missing the colon.** The loop header ends with `:`. Every time. Python's error message for this is more helpful than it looks once you know what you are looking at.
- **Wrong indentation.** If the body is not indented past the header, Python does not know it belongs to the loop. If a line is indented when it should not be, it runs on every pass instead of once at the end.
- **Forgetting to increment.** Only a `while` loop problem, and only ever solved by Ctrl-C and a sigh.

## Where this leaves you

The short version: reach for a `for` loop when you have a sequence to go through or a fixed number of repetitions, and a `while` loop when you are waiting for a condition to change. Use `break` to leave early and `continue` to skip an item.

If you are learning this for security work, this is genuinely a large chunk of the job. Checking a list of devices against an approved list, going through log entries one at a time, stopping as soon as you find the thing you were looking for. It is all loops. The syntax stops feeling strange faster than you would expect, and then you get to spend your attention on the actual problem instead of on typing the same line four times.

**Best way to make any of this stick:** open a Python file and retype these examples by hand instead of copying them. Then break one on purpose and read what Python tells you.
