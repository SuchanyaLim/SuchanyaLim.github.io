---
layout: default
---

## Command-line Tools for Linguists (KIK-LG221)

<img src="https://images.unsplash.com/photo-1629654291663-b91ad427698f?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1374" alt="Photo of cmdline" hspace="20" width="30%" align="right"/>

The command-line tools for linguists course introduces linguists to working in the command-line. The course goes over command-line basics, text processing, scripting, remote access, and version control.

I highly recommend this course for anyone who needs some guided introduction to command-line magic and text processing workflows!

### Module 1: Introduction to Command Line Environments

As the name says, Module 1 was an introduction to command-line environments. We went over how to set up our command-line environment ([WSL 2 for Windows users!](https://www.youtube.com/watch?v=8wDXqM_YjT0&t=1s)) and basic commands for navigating the command-line. We also learned about the Unix file system.

We used commands like `ls` to list files, `cat` and `nano` to view and edit files. We covered file management commands such as `cp` to copy or `mv` to move files, `mkdir` to create directories and `cd` to navigate between them. We also learned about users, groups, and file permissions and using `chmod` to change file read, write, and execute permissions. Finally, we looked at `curl` for downloading text files which we will use for text processing in Module 2.

This week was a good refresher for those who have used the command-line before. It was helpful to have everything explained in context. What I found most helpful was setting up WSL 2 as that had always intimidated me for some reason. I also appreciated the explanation on groups and file permissions.

### Module 2: Text Processing in UNIX
The module titles are aptly named, in Module 2 we went over text processing in a UNIX system and the differences between UNIX and DOS (Windows). We learn about character-encodings, and commands for processing and searching text files: `grep` and `sed`. Finally, we learn how to turn long texts into structured text-files.

This module made text processing in a command-line environment easy to understand. We also learned how to chain command-line commands using pipes (`|`).

Commands used in this Module:
- `grep` - search for text patterns in a file
- `sed` - perform text transformations
- `cut` - extract columns from files
- `tr` - translate or delete characters

Here is a Cheatsheet for commonly used regex expressions

| Regex       | Description                                                | Examples                                                        |
| ----------- | ---------------------------------------------------------- | --------------------------------------------------------------- |
| `^a`        | Matches 'a' at the beginning of a string/line              | `apple`, `ant`                                                  |
| `$a`        | Matches 'a' at the end of a string/line                    | `banana`, `a`                                                   |
| `\d`        | Matches any single digit (0-9)                             | `1`, `2`, `7`                                                   |
| `\b`        | Matches word boundary (position between word and non-word) | `\bcat\b` would match `cat` in "the cat" but not in "catacombs" |
| `[:alpha:]` | Matches any letter (A-Z, a-z)                              | `A`, `b`, `Z`                                                   |
| `[:digit:]` | Matches any digit (0-9)                                    | `4`, `7`, `9`                                                   |
| `[:punct:]` | Matches any punctuation character                          | `.`, `!`, `;`, `,`                                              |
| `a*`        | Matches zero or more occurrences of 'a'                    | `ca*` would match c, ca, caa, etc.                              |
| `a+`        | Matches one or more occurrences of 'a'                     | `ca+` would match ca, caa, caaa, etc.                           |
| `a?`        | Matches zero or one occurrence of 'a'                      | `caa?t` would match both cat and caat                           |
| `.`         | Matches any character (except newline)                     | `a`, `1`, `!`, `Z`                                              |
| `(a\|b)`    | Matches either 'a' or 'b'                                  | `ca(b\|t)` would match both cat and cab                         |
| `[abc]`     | Matches any of 'a', 'b', or 'c'                            | `c[abc]t` would match cat, cbt, cct                             |
| `[^abc]`    | Matches any character except 'a', 'b', or 'c'              | `c[^abc]t` would match anything except cat, cbt, cct            |
| `[a-zA-Z]`  | Matches any letter (lowercase or uppercase)                | `a`, `Z`, `r`, `T`                                              |
| `[0-9]`     | Matches any digit from 0 to 9                              | `3`, `8`, `5`                                                   |

#### The `Sed` Command
I would say the most difficult part of this Module was the `sed` command. `sed` apparently has multiple commands, but the one we focus on in this module is substitution. `sed` allows you to replace patterns (regex) in a text. The command usually looks like `sed 's/A/B/' file.txt`. This will replace the first occurrence of A on each line to B.
Let's say we have a `file.txt`
```
I love apples! Apples are nice.
Apples are my favorite.
```
and we use the sed command on it like so:
```
sed 's/apples/oranges/' file.txt
```
the output would look like:
```
I love oranges! Apples are nice.
Apples are my favorite.
```
This is because `sed` is case-sensitive and will only replace the first match on each line.

Now this is just a short overview, `sed` is very powerful and quite complex. You can check out [this site](https://www.grymoire.com/Unix/Sed.html) for a more comprehensive explanation of `sed` commands.
