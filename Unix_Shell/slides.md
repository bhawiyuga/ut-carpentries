---
marp: true
theme: default
paginate: true
header: 'Unix Shell Training'
footer: 'Software Carpentries - The Unix Shell'
style: |
  section {
    font-size: 24px;
  }
  h1 {
    font-size: 42px;
    color: #2c3e50;
  }
  h2 {
    font-size: 34px;
    color: #34495e;
  }
  code {
    font-size: 18px;
    background-color: #f4f4f4;
    padding: 2px 6px;
    border-radius: 4px;
  }
  pre {
    background-color: #f8f8f8;
    border-left: 4px solid #3498db;
    padding: 8px;
    font-size: 18px;
  }
  table {
    font-size: 22px;
  }
---

<!-- _class: lead -->
# The Unix Shell
## A Training Slide Deck

**Based on Software Carpentries: The Unix Shell**

---

<!-- _class: lead -->
# Episode 1
## Introducing the Shell

---

# What is the Shell?

- **GUI (Graphical User Interface)**: Clicking and menus - intuitive but scales poorly
- **CLI (Command-Line Interface)**: Text-based interaction - fast and automatable
- **Shell**: A program that reads commands and runs other programs
- This workshop uses **Bash** - the most popular Unix shell

> "The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines."

---

# Why Use the Shell?

**Example Task**: Copy the third line from 1,000 text files in 1,000 different directories into a single file.

| GUI Approach | CLI Approach |
|-------------|--------------|
| Hours of clicking | One series of commands |
| Error-prone | Consistent and instant |
| Not reproducible | Can be saved as a script |

The shell excels at:
- Automating repetitive tasks
- Combining tools together
- Running programs on remote systems

---

# The Shell Prompt

When you open the shell, you see a **prompt**:

```bash
$
```

- The `$` indicates the shell is waiting for input
- **Do not type the prompt** - only type the command after it
- Press **Enter** to execute a command
- Your prompt might look like: `nelle@localhost $`

---

# Your First Command: `ls`

Try listing the contents of your current directory:

```bash
$ ls
```

Output:
```
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

If the shell can't find a program, you'll see:
```bash
$ ks
ks: command not found
```

---

# Key Points: Introducing the Shell

- A **shell** is a program whose primary purpose is to read commands and run other programs
- This lesson uses **Bash**, the default shell in many Unix implementations
- Programs can be run in Bash by entering commands at the **command-line prompt**
- The shell excels at: high action-to-keystroke ratio, automating repetitive tasks, and accessing networked machines
- A significant challenge is **knowing what commands to run and how to run them**

---

<!-- _class: lead -->
# Episode 2
## Navigating Files and Directories

---

# The File System

- The **file system** manages files and directories
- **Files** hold information
- **Directories** (folders) hold files or other directories
- Organized as a tree with the **root directory** `/` at the top

```
/
├── bin/
├── data/
├── Users/
│   ├── nelle/
│   ├── imhotep/
│   └── larry/
└── tmp/
```

---

# Essential Navigation Commands

| Command | Description | Example |
|---------|-------------|---------|
| `pwd` | **P**rint **W**orking **D**irectory | `pwd` → `/Users/nelle` |
| `ls` | **L**i**s**t directory contents | `ls`, `ls -F`, `ls -a` |
| `cd` | **C**hange **D**irectory | `cd Desktop`, `cd ..` |

```bash
$ pwd
/Users/nelle

$ ls -F
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
```

---

# Absolute vs. Relative Paths

**Absolute Path**: Starts from root `/`
```bash
$ cd /Users/nelle/Desktop/shell-lesson-data
```

**Relative Path**: Starts from current directory
```bash
$ cd Desktop/shell-lesson-data/exercise-data
```

---

# Special Directory Shortcuts

| Symbol | Meaning | Example |
|--------|---------|---------|
| `.` | Current directory | `ls .` |
| `..` | Parent directory | `cd ..` |
| `~` | Home directory | `cd ~` |
| `-` | Previous directory | `cd -` |

```bash
$ cd ..      # Go up one level
$ cd ~       # Go to home directory
$ cd -       # Go back to previous directory
$ cd         # Also goes to home directory
```

---

# Command Syntax

```bash
$ ls -F /
```

- `ls` = **command**
- `-F` = **option** (flag/switch) - changes behavior
- `/` = **argument** - tells command what to operate on

Options:
- **Short options**: single dash `-F`, `-a`, `-l`
- **Long options**: double dash `--help`

Multiple options can be combined: `ls -Fa` = `ls -F -a`

---

# Getting Help

```bash
# Option 1: --help flag
$ ls --help

# Option 2: man pages (Linux, macOS)
$ man ls
```

**Navigating man pages**:
- ↑ / ↓ - move line by line
- Spacebar / b - page up/down
- `/word` - search for "word"
- N / Shift+N - next/previous match
- q - quit

---

# Tab Completion

The shell can auto-complete file and directory names:

```bash
$ ls nor<TAB>
# Expands to:
$ ls north-pacific-gyre/

$ ls north-pacific-gyre/g<TAB>
# Expands to:
$ ls north-pacific-gyre/goo

$ ls north-pacific-gyre/goo<TAB><TAB>
goodiff.sh   goostats.sh
```

**Tab completion reduces typing errors and saves time!**

---

# Key Points: Navigating Files and Directories (1)

- The **file system** manages information on disk in files and directories
- `pwd` prints your **current working directory**
- `ls [path]` lists contents of a specific file or directory
- `cd [path]` changes your current working directory

---

# Key Points: Navigating Files and Directories (2)

- Most commands take **options** (begin with `-`) and **arguments**
- **Absolute paths** start from `/`; **relative paths** start from current location
- `.` = current directory, `..` = parent directory
- Use **tab completion** to minimize typing and errors

---

<!-- _class: lead -->
# Episode 3
## Working With Files and Directories

---

# Creating Directories and Files

**Create a directory:**
```bash
$ mkdir thesis              # Create single directory
$ mkdir -p ../project/data  # Create nested directories
```

**Create an empty file:**
```bash
$ touch my_file.txt
```

**Edit a file with nano:**
```bash
$ nano draft.txt
# Ctrl+O to save, Ctrl+X to exit
```

---

# Moving and Renaming

`mv` moves or renames files and directories:

```bash
# Rename a file
$ mv thesis/draft.txt thesis/quotes.txt

# Move a file to current directory
$ mv thesis/quotes.txt .

# Move multiple files
$ mv sucrose.dat maltose.dat ../raw
```

⚠️ **Warning**: `mv` silently overwrites existing files. Use `-i` for confirmation:
```bash
$ mv -i old.txt new.txt
```

---

# Copying Files and Directories

`cp` copies files:

```bash
# Copy a file
$ cp quotes.txt thesis/quotations.txt

# Copy to a directory (keeps original name)
$ cp quotes.txt thesis/

# Copy a directory recursively
$ cp -r thesis thesis_backup
```

⚠️ **Remember `-r`** for directories! Without it:
```bash
$ cp thesis thesis_backup
cp: -r not specified; omitting directory 'thesis'
```

---

# Removing Files

`rm` removes files **permanently** (no trash bin!):

```bash
# Remove a file
$ rm quotes.txt

# Remove with confirmation
$ rm -i thesis_backup/quotations.txt
```

⚠️ **There is no undo!** Deleted files are gone forever.

---

# Removing Directories

```bash
# Remove a directory and ALL its contents
$ rm -r thesis

# Remove with confirmation recursively
$ rm -r -i thesis
```

⚠️ **Use with great caution!** `rm -r` deletes everything without asking.

---

# Using Wildcards

Wildcards help work with multiple files at once:

| Wildcard | Meaning | Example |
|----------|---------|---------|
| `*` | Zero or more characters | `*.txt` matches all `.txt` files |
| `?` | Exactly one character | `?.txt` matches `a.txt` but not `any.txt` |

The **shell expands wildcards** before running the command!

---

# Wildcard Examples

```bash
# List all .pdb files
$ ls *.pdb

# List files starting with 'c'
$ ls c*

# Files with exactly 3 chars before 'ane.pdb'
$ ls ???ane.pdb
```

**Common use case** - move all `.dat` files:
```bash
$ mv *.dat analyzed/
```

---

# Good File Naming Practices

1. **Don't use spaces** - use `-` or `_` instead
   - Bad: `north pacific gyre/`
   - Good: `north-pacific-gyre/`

2. **Don't start with `-`** - commands will treat it as an option

3. **Stick with**: lowercase letters, numbers, `.`, `-`, `_`
   - Many characters have special meanings

4. **Use meaningful extensions**:
   - `.txt` for text files
   - `.csv` for comma-separated values
   - `.sh` for shell scripts

---

# Key Points: Working With Files

- `cp [old] [new]` - copy a file
- `mkdir [path]` - create a new directory
- `mv [old] [new]` - move/rename a file or directory
- `rm [path]` - remove/delete a file
- `*` matches zero or more characters; `?` matches any single character
- Use **Control key** combinations: `Ctrl+O`, `Ctrl+X`, etc.
- **The shell has no trash bin** - deletions are permanent
- Use consistent, simple filenames to make wildcard matching easier

---

<!-- _class: lead -->
# Episode 4
## Pipes and Filters

---

# The Power of Combining Commands

Unix philosophy: **Many simple tools that each do one job well, and work well together.**

**Filters** are programs that transform input into output:
- `wc` - word count
- `sort` - sort lines
- `head` / `tail` - show first/last lines
- `cat` - concatenate/display files
- `cut` - extract columns

---

# Counting with `wc`

```bash
# Count lines, words, and characters
$ wc cubane.pdb
20  156  1158  cubane.pdb

# Count only lines
$ wc -l *.pdb
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
 107  total
```

Options:
- `-l` = lines only
- `-w` = words only
- `-m` = characters only

---

# Redirecting Output

Save command output to a file instead of printing to screen:

```bash
# Redirect > (OVERWRITES file!)
$ wc -l *.pdb > lengths.txt

# Append >>
$ echo "hello" >> log.txt

# View file contents
$ cat lengths.txt
```

⚠️ **Warning**: `>` overwrites existing files without warning!

```bash
# BAD idea - may corrupt data:
$ sort -n lengths.txt > lengths.txt
```

---

# Pipes: Connecting Commands

The pipe `|` sends the output of one command as input to another:

```bash
# Without pipes (using intermediate files)
$ wc -l *.pdb > lengths.txt
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt

# With pipes - much cleaner!
$ wc -l *.pdb | sort -n | head -n 1
```

**Read pipes left to right**: "head of sort of line count of `*.pdb`"

---

# Useful Filter Commands

```bash
# sort - sort lines
$ sort -n lengths.txt      # numerical sort
$ sort -r file.txt         # reverse sort

# head / tail - show parts of files
$ head -n 5 file.txt       # first 5 lines
$ tail -n 3 file.txt       # last 3 lines

# less - view file page by page
$ less lengths.txt         # q to quit

# cut - extract columns
$ cut -d , -f 2 animals.csv   # 2nd field, comma-delimited
```

---

# Example Pipeline

**Find the 3 files with the fewest lines:**

```bash
$ wc -l * | sort -n | head -n 3
```

**Find unique values in a CSV column:**

```bash
$ cut -d , -f 2 animals.csv | sort | uniq
```

**Count occurrences:**

```bash
$ cut -d , -f 2 animals.csv | sort | uniq -c
```

---

# Key Points: Pipes and Filters

- `wc` counts lines, words, and characters
- `cat` displays file contents; `less` shows page by page
- `sort` sorts input; `head`/`tail` show first/last lines
- `command > file` redirects output to a file (overwrites)
- `command >> file` appends output to a file
- `[first] | [second]` is a **pipeline** - output of first becomes input of second
- The best way to use the shell is to combine simple single-purpose programs with pipes

---

<!-- _class: lead -->
# Episode 5
## Loops

---

# Why Loops?

**Loops** repeat commands for each item in a list - essential for automation!

**Example**: Print the classification from each of 3 data files:

Without a loop:
```bash
$ head -n 2 basilisk.dat | tail -n 1
$ head -n 2 minotaur.dat | tail -n 1
$ head -n 2 unicorn.dat | tail -n 1
```

With a loop:
```bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     echo $filename
>     head -n 2 $filename | tail -n 1
> done
```

---

# Loop Syntax

```bash
for variable in list_of_items
do
    command_using $variable
done
```

**Key concepts:**
- The **variable** holds each item in turn
- `$variable` expands to the current value
- `${variable}` also works (safer when concatenating)

```bash
# Example: print numbers 0-9
$ for loopvar in 0 1 2 3 4 5 6 7 8 9
> do
>     echo $loopvar
> done

# Shorthand using brace expansion
$ for loopvar in {0..9}
```

---

# Looping Over Files

Use wildcards to create file lists:

```bash
# Process all .dat files
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```

**Practical example** - backup files with prefix:
```bash
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

Result: `basilisk.dat` → `original-basilisk.dat`

---

# Debugging Loops with `echo`

Preview what a loop *would* do without actually running it:

```bash
# What would this loop do?
$ for datafile in *.pdb
> do
>     echo "cat $datafile >> all.pdb"
> done

cat cubane.pdb >> all.pdb
cat ethane.pdb >> all.pdb
cat methane.pdb >> all.pdb
...
```

> **Tip**: Using quotes around the entire command makes `>>` literal text, not a redirection!

---

# History Shortcuts

| Shortcut | Action |
|----------|--------|
| ↑ / ↓ | Scroll through previous commands |
| `history` | List recent commands |
| `!123` | Re-run command number 123 |
| `!!` | Re-run last command |
| `!$` | Last word of last command |
| Ctrl+R | Search command history |
| Ctrl+A | Go to start of line |
| Ctrl+E | Go to end of line |

---

# Nested Loops

Loops can contain other loops:

```bash
$ for species in cubane ethane methane
> do
>     for temperature in 25 30 37 40
>     do
>         mkdir $species-$temperature
>     done
> done
```

Creates directories:
- `cubane-25`, `cubane-30`, `cubane-37`, `cubane-40`
- `ethane-25`, `ethane-30`, ...
- `methane-25`, `methane-30`, ...

---

# Key Points: Loops (1)

- A `for` loop repeats commands once for every item in a list
- Every loop needs a **variable** (`$name`) to refer to the current item
- Use `$name` or `${name}` to expand a variable
- **Don't use spaces** in filenames - it complicates variable expansion

---

# Key Points: Loops (2)

- Give files **consistent names** that are easy to match with wildcards
- Use **↑** to scroll through previous commands
- Use **Ctrl+R** to search command history
- Use `history` and `![number]` to repeat commands

---

<!-- _class: lead -->
# Episode 6
## Shell Scripts

---

# What is a Shell Script?

A **shell script** is a file containing multiple shell commands that can be executed together.

**Benefits:**
- Save and reuse commands
- Avoid retyping
- Make work reproducible
- Share with others

---

# Creating and Running a Script

**Create a script with nano:**
```bash
$ nano middle.sh
```

Add commands to the file:
```bash
head -n 15 octane.pdb | tail -n 5
```

**Run the script:**
```bash
$ bash middle.sh
```

---

# Using Command-Line Arguments

Scripts can accept arguments using special variables:

| Variable | Meaning |
|----------|---------|
| `$1` | First argument |
| `$2` | Second argument |
| `$3` | Third argument |
| `$@` | All arguments |

**Example** - `middle.sh`:
```bash
head -n "$2" "$1" | tail -n "$3"
```

Usage:
```bash
$ bash middle.sh pentane.pdb 15 5
```

---

# Writing Better Scripts

Add **comments** to explain what your script does:

```bash
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
```

**Tips:**
- Start comments with `#`
- Quotes around `"$1"` handle filenames with spaces
- `"$@"` is special syntax for all arguments (equivalent to `"$1" "$$2" ...`)

---

# Example: Sorting Script

```bash
# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

Run it:
```bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

Output:
```
9 methane.pdb
12 ethane.pdb
15 propane.pdb
...
596 total
```

---

# Capturing History

Save your recent commands to a script:

```bash
$ history | tail -n 5 > redo-analysis.sh
```

Then edit to:
- Remove line numbers
- Remove the `history` command itself
- Add comments

This is a common workflow: experiment interactively, then capture the successful commands in a script.

---

# Key Points: Shell Scripts

- Save commands in **shell scripts** for re-use
- `bash [filename]` runs the commands saved in a file
- `$@` refers to **all** command-line arguments
- `$1`, `$2`, etc. refer to the first, second, etc. arguments
- **Quote variables** if values might contain spaces
- Let users decide what files to process - more flexible and consistent with Unix commands
- Add **comments** starting with `#` to explain your scripts

---

<!-- _class: lead -->
# Episode 7
## Finding Things

---

# Finding Text with `grep`

`grep` finds and prints lines matching a pattern:

```bash
$ grep not haiku.txt
Is not the true Tao, until
"My Thesis" not found
Today it is not working
```

By default, `grep` searches case-sensitively and matches partial words.

---

# `grep` Options

```bash
# Word boundaries only
$ grep -w The haiku.txt
The Tao that is seen

# Case-insensitive
$ grep -i "the" haiku.txt

# Inverted search (lines that DON'T match)
$ grep -v "the" haiku.txt

# With line numbers
$ grep -n "it" haiku.txt
```

---

# `grep` Options Summary

| Option | Meaning |
|--------|---------|
| `-w` | Match whole words only |
| `-i` | Case-insensitive |
| `-n` | Show line numbers |
| `-v` | Invert match (show non-matching lines) |
| `-r` | Recursive (search directories) |
| `-E` | Extended regular expressions |

```bash
# Search recursively in all .txt files
$ grep -r "Yesterday" .

# Combine options
$ grep -n -w -i "the" haiku.txt
```

---

# Finding Files with `find`

`find` locates files and directories by name or type:

```bash
# List all files and directories
$ find .

# Find only directories
$ find . -type d

# Find only files
$ find . -type f

# Find by name (quote wildcards!)
$ find . -name "*.txt"

# Find by name case-insensitive
$ find . -iname "*.TXT"
```

⚠️ **Always quote wildcards** in `find` so the shell doesn't expand them!

---

# Combining `find` with Other Commands

Use `$()` to use command output as arguments:

```bash
# Count lines in all .txt files
$ wc -l $(find . -name "*.txt")

# Search for text in all .txt files
$ grep "searching" $(find . -name "*.txt")
```

**How it works:**
1. Shell runs the command inside `$()`
2. Replaces `$()` with the command's output
3. Runs the outer command with that output

---

# `grep` with Regular Expressions

`grep`'s real power comes from **regular expressions**:

```bash
# Find lines with 'o' in the second position
$ grep -E "^.o" haiku.txt
You bring fresh toner.
Today it is not working
Software is like that.
```

| Pattern | Meaning |
|---------|---------|
| `^` | Start of line |
| `.` | Any single character |
| `*` | Zero or more of the preceding |

> See the Library Carpentry regular expressions lesson for more!

---

# Example: Finding and Filtering

**Find all `.dat` files except those containing "unicorn":**

```bash
$ find creatures -name "*.dat" | grep -v unicorn
```

**Find files and count lines:**
```bash
$ wc -l $(find . -name "*.dat") | sort -n
```

**Find text in specific files:**
```bash
$ grep "pattern" $(find . -name "*.txt")
```

---

# Key Points: Finding Things

- `find` finds files with specific properties that match patterns
- `grep` selects lines in files that match patterns
- `--help` displays usage information for many commands
- `man [command]` displays the manual page for a command
- `$([command])` inserts a command's output in place
- **Quote wildcards** in `find` to prevent shell expansion
- Regular expressions make `grep` extremely powerful for pattern matching

---

<!-- _class: lead -->
# Summary
## The Unix Shell

---

# Command Reference

| Command | Purpose |
|---------|---------|
| `pwd` | Print working directory |
| `ls` | List directory contents |
| `cd` | Change directory |
| `mkdir` | Make directory |
| `cp` | Copy files/directories |
| `mv` | Move/rename files/directories |
| `rm` | Remove files/directories |
| `cat` | Display file contents |
| `wc` | Count lines/words/characters |
| `sort` | Sort lines |
| `head` / `tail` | Show first/last lines |
| `grep` | Find matching text |
| `find` | Find files by name/type |

---

# Concepts Reference

| Concept | Description |
|---------|-------------|
| **Absolute path** | Starts from `/` |
| **Relative path** | Starts from current directory |
| **Wildcards** | `*` = any chars, `?` = one char |
| **Redirection** | `>` = overwrite, `>>` = append |
| **Pipes** | `\|` = connect command output to input |
| **Variables** | `$name` or `${name}` |
| **Loops** | `for ... do ... done` |
| **Scripts** | Save commands in a file, run with `bash` |

---

<!-- _class: lead -->
# Thank You!

## The Unix Shell

**Materials:** https://swcarpentry.github.io/shell-novice/

**Licensed under CC-BY 4.0 by The Carpentries**
