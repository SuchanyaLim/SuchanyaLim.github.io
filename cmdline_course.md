---
layout: default
---

## Command-line Tools for Linguists (KIK-LG221)

<img src="https://images.unsplash.com/photo-1629654291663-b91ad427698f?ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&q=80&w=1374" alt="Photo of cmdline" hspace="20" width="40%" align="right"/>

The command-line tools for linguists course introduces linguists to working in the command-line. The course goes over command-line basics, text processing, scripting, remote access, and version control.

I highly recommend this course for anyone who needs some guided introduction to command-line magic and text processing workflows!

### Module 1: Introduction to Command Line Environments
As the name says, Module 1 was an introduction to command-line environments. We went over how to set up our command-line environment ([WSL 2 for Windows users!](https://www.youtube.com/watch?v=8wDXqM_YjT0&t=1s)) and basic commands for navigating the command-line. We also learned about the Unix file system.

We used commands like `ls` to list files, `cat` and `nano` to view and edit files. We covered file management commands such as `cp` to copy or `mv` to move files, `mkdir` to create directories and `cd` to navigate between them. We also learned about users, groups, and file permissions and using `chmod` to change file read, write, and execute permissions. Finally, we looked at `curl` for downloading text files which we will use for text processing in Module 2.

This week was a good refresher for those who have used the command-line before. It was helpful to have everything explained in context. What I found most helpful was setting up WSL 2 as that had always intimidated me for some reason. I also appreciated the explanation on groups and file permissions.

#### The UNIX File System
The UNIX File system has a few differences from Windows. `/bin` and `/home` are two important directories we often encounter. `/bin` contains executables (which can be programs, or commands we use like `ls`), while `/home` is where a user's personal files are stored. 

A UNIX computer can have several users with different permissions. The `root` user has the highest privileges and can make system-wide changes like installing packages or software and modifying files. 

Users can also be organized into groups, which makes it easy to set file permissions for multiple users at once. A file can have permissions, specifically: 
- Read (`r`): can view file
- Write (`w`): can edit or delete file
- Execute (`x`): can run the file

You can change file permissions using the command `chmod`, for example:
```
chmod u+r file.txt
```
This gives the user (owner) read-only access to a file. You can also set multiple permissions at once:
```
chmod u=rx,g=r file.txt
```
This would allow the user to read and execute the file, while giving group members read-only access.

Execute permissions are especially important for making shell scripts executable (so we can use them!), which we will go over in Module 3 (scripting).

### Module 2: Text Processing in UNIX
The module titles are aptly named, in Module 2 we went over text processing in a UNIX system and the differences between UNIX and DOS (Windows). We learn about character-encodings, and commands for processing and searching text files: `grep` and `sed`. Finally, we learn how to turn long texts into structured text-files.

This module made text processing in a command-line environment easy to understand. We also learned how to chain command-line commands using pipes (`|`).

Commands used in this Module:
- `grep` - search for text patterns in a file
- `sed` - perform text transformations
- `cut` - extract columns from files
- `tr` - translate or delete characters

Here is a Cheatsheet for some common regex expressions

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
`sed` would replace 'apples' with 'oranges' and the output would look like:
```
I love oranges! Apples are nice.
Apples are my favorite.
```
This is because `sed` is case-sensitive and only works on the first match on each line, so it can only replace 'apples' and not 'Apples' on the second line.

Now this is just a short overview, `sed` is very powerful and quite complex. You can check out [this site](https://www.grymoire.com/Unix/Sed.html) for a more comprehensive explanation of `sed` commands.

#### Text Processing Pipelines
This is one of the more important parts of the course for linguists. We learned how to implement simple text processing pipelines using the pipe `|` to connect commands to turn raw text into useful data for analysis. 

As a little introduction: using the `tr` command, we learned how to convert a text file into a word frequency list to see how often each word appears.
```
cat file.txt | tr -s '\n\r\t ' '\n' | tr -dc "A-Za-z0-9\n'" | sort | uniq -c | sort -nr > text.freq
```
With the pipe, we can direct the output of `cat text.txt` (which is the entire file contents), to the next command `tr`. The command `tr` transforms text similar to "find and replace" in text editors. 
- `tr -s '\n\r\t ' '\n'` replaces newline (`\n`), return (`\r`), tab (`\t`), and space characters with a newline, creating a one-word-per-line file. The `-s` option squeezes repeated spaces or blank lines into a single newline. 
- We use `tr` again with the `-d` and `-c` options to delete characters not in `"A-Za-z0-9\n'"`. This will remove punctuation and keep only characters that are part of a word. 
- Then, we `sort` the words alphabetically so that `uniq -c` can count duplicates (`-c` will add the number of times the word occurs before each word). 
- We `sort` again using `-nr` to order the results numerically and in reverse (so that the most frequent words are at the top). 
- Finally, we direct our output to a file called `text.freq`
This might seem long and a bit overwhelming, but it's a straightforward way to turn plain text into structured data using only a few commands.

In this chapter, we also learned how to compute sentence-level statistics by generating a "sentence-per-line" file using `sed` and a similar process for word n-grams (sequences of n consecutive words) which are commonly used in language technology. Although I will leave those examples out so this section does not get too long.

### Module 3: Scripting, Configuration Files and Installing Programs
In Module 3, the focus was on scripts. Scripts allow us to take the single-line commands we typically use and combine them into reusable, organized snippets. Writing scripts allow us to easily edit and run sequences of commands.

We also learn about environment variables in UNIX systems. These variables control how programs behave. We modify them and save the changes in our configuration file to keep the changes permanent. 

Finally, we learned about becoming a root user, which gives us full administrative privileges, and how we can install software through package managers like `apt`. We also covered installing Python packages via `pip`.

Scripting was one of the topics I was looking forward to most as it can be very useful for automating both personal tasks and research. And learning about how to change and save environment variables has opened a lot of opportunities for tinkering with my system which is kind of overwhelming in a way. Installing software from the command-line using `apt` and installing Python packages with `pip` was relatively straightforward in comparison.
#### Scripting Overview
In a UNIX environment, **scripting** typically refers to writing **bash scripts**. A script is a sequence of commands written in a file, which can be executed as a program. To indicate that it’s a bash script, we start the file with `#!/bin/bash` (referred to as the 'shebang') to tell the system that the script should be run using bash.

As with other programming languages, bash scripts also have syntax for loops, conditionals, and input. Scripts can take input from the command line using special variables. For example, `$1`, `$2`, etc., represent arguments passed to the script:
```bash
#!/bin/bash
echo "The first argument is: $1"
```
If you run this script like:
```bash
./myscript.sh hello
```
It would output:
```bash
The first argument is: hello
```
##### Running a Script
To run a script, you have to make the script executable by using `chmod`:
```bash
chmod 755 myscript.sh
```
`755` is often used to grant the owner write or modify permissions and allow everyone else to execute the script. Then you can run the script using:
```bash
./myscript.sh
```
This will run the script that is in your current directory (`./`). It is important to specify the path of your script because Bash usually looks for commands in your $PATH variable. If your current directory is not in the $PATH, bash will not find it.

### Module 4: Using `ssh`, `scp`, and Version Control
In Module 4 we looked at connecting to a remote server and version control with Git. We also learned about processes. 

This Module was packed with valuable tools I expect to use regularly. I’ve always wanted to learn SSH and Git, but found the concepts a bit overwhelming at first. After using both for this course, I realized they’re not as complex as I feared. Now I feel much more comfortable with them and am looking forward to using them in my personal projects.

#### Remote Access with SSH
`ssh` or Secure Shell is used to connect to remote servers, then you can work on files there as if it were your own computer! This is especially useful for research when you don’t have enough computational power on your own machine. For example, by `ssh`-ing into rental cloud-based systems like CSC, you can take advantage of their processing power to run resource-intensive tasks in minutes. 
When using `ssh`, we also explored public and private keys, which are used for authentication. Setting up passwordless SSH allows for more secure and convenient connections.

We also learned about `scp`, the Secure Copy Protocol which allows us to copy files to and from remote servers.

#### Version Control with Git
Finally, Git. Git is one of the most widely used software. Git is a version control system used to manage code. It allows you to organize your work, track changes to your files, and collaborate with others! This can make it seem overwhelming, but it becomes easier once you start using it. While Git can be used locally, its more often used with remote repositories such as GitHub that make it easier to share code and collaborate with others. I recommend [this video](https://www.youtube.com/watch?v=HVsySz-h9r4) for an easy-to-follow tutorial for Git and GitHub. For those who don't have a GitHub account yet, it's free and easy to setup: [go to GitHub site](https://github.com). 

Here are some Git commands to get started:
- **`git clone`**: Clone a remote repository to your local machine.
- **`git pull`**: Get the latest changes from the remote repository and merge them into your local branch.
- **`git add`**: Stage changes to prepare them for commit. Use **`git reset`** if you need to unstage something.
- **`git status`**: Check the current status of your working directory.
- **`git log`**: View the commit history of the repository.
- **`git commit -m "message"`**: Commit changes with a message describing what was done.
- **`git branch`**: Create a new branch to work on a feature or bug fix.
- **`git checkout`**: Switch between branches.
- **`git merge`**: Merge a branch into the main branch.

#### Jekyll and GitHub Pages
GitHub pages use Jekyll as its backend to generate a website directly from a GitHub repository. Jekyll is a Ruby-based static site generator that allows you to create a website using markdown files for content. To create a GitHub page, you need to:
1. Create a GitHub repository
	- The easiest is to setup a repository using your username in the format `username.github.io` 
	- OR you could enable GitHub Pages for an existing repository in the repository's settings by selecting the source for GitHub Pages (usually `main`, `/docs`, or a separate branch).
2. Create a `_config.yml`
	- This file contains settings for your site, such as a **title**, **description**, or a [**Jekyll theme**](https://jekyllthemes.io).
```
title: Title of Your Site
description: a short description
theme: jekyll-theme-slate
```
Here is an example of a `_config.yml` file.
3. Create your 'home page'
	- This is usually an `index.md` file.
	- You write your file in [Markdown](https://www.markdown-cheatsheet.com) and GitHub will automatically render it into HTML!
4. Push to GitHub!
	- Once you have your `_config.yml` and `index.md` files, you can push them to your repository.
	- You can create other pages and link to them using Markdown's link syntax. Any `.md` files you create will automatically be converted to HTML by Jekyll when pushed to GitHub as long as they are in the correct directory.
GitHub Pages automatically builds and serves the HTML pages for you based on the content and structure you've set up. By default, Jekyll applies the `default` layout to pages unless you specify something else in the frontmatter of your file. You can create custom layouts by adding `.html` files to the `_layouts/` folder and adjusting the frontmatter of your file accordingly.

...and that's the course! We covered a lot of content, but there is still so much more to learn. Thank you for reading, I hope you found it helpful and that you'll consider this course as well.
