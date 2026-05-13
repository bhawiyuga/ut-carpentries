---
marp: false
theme: uncover
class:
  - lead
paginate: true
backgroundColor: #fff
style: |
  section {
    font-size: 1.5em;
  }
  section.title {
    --title-color: #2c3e50;
    color: var(--title-color);
  }
  code {
    background: #f4f4f4;
    border-radius: 4px;
    padding: 2px 6px;
  }
  pre {
    background: #2d2d2d;
    color: #f8f8f2;
    padding: 16px;
    border-radius: 8px;
    font-size: 0.8em;
  }
  section.episode-header {
    background: #2c3e50;
    color: white;
  }
---

<!-- _class: episode-header -->
# The Unix Shell
## A Hands-on Training

<!--
Welcome to our training on the Unix Shell. Over the next sessions, we'll learn how to use the command line to automate tasks and work more efficiently.
-->

---

<!-- _class: episode-header -->
# Episode 1
## Introducing the Shell

---

## What is a Shell?

- A **program** that lets you type commands
- Reads commands and runs other programs
- **Bash** — the most popular Unix shell
- Text-based interface: **Command-Line Interface (CLI)**

![width:500px](https://upload.wikimedia.org/wikipedia/commons/4/4b/Bash_Logo_Colored.svg)

---

## GUI vs CLI

<!-- _class: split -->

<div style="display: flex; gap: 40px;">

<div style="flex: 1;">

### GUI
- Mouse clicks
- Menu-driven
- Intuitive to learn
- **Doesn't scale** for repetitive tasks

</div>

<div style="flex: 1;">

### CLI
- Text commands
- Keyboard-driven
- Takes effort to learn
- **Excellent** for automation

</div>

</div>

---

## Why Use the Shell?

- **Automate repetitive tasks** — copy the 3rd line of 1000 files in seconds
- **Reproducibility** — save commands as scripts
- **Remote access** — cloud, clusters, servers
- **High action-to-keystroke ratio** — do more with fewer keystrokes
- **Combine tools** — chain simple programs together

---

## The Shell Prompt

```bash
$
```

- The `$` indicates the shell is waiting for input
- **Do not type the prompt** — only type the command that follows
- Press **Enter** to execute a command
- Your prompt may look different (e.g., `user@hostname $`)

---

## First Command: `ls`

```bash
$ ls
```

```
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

- `ls` = **list** — shows the contents of the current directory
- Try it! Type `ls` and press Enter

---

## Command Not Found

```bash
$ ks
```

```
ks: command not found
```

- If the shell can't find the command, it prints an error
- Possible causes:
  - Typo in the command name
  - Program not installed
  - Wrong path

---

## Nelle's Pipeline: A Typical Problem

- **Nelle Nemo**, marine biologist
- 1520 samples from the North Pacific Gyre
- Needs to run `goostats.sh` on each file
- **Manual**: 12+ hours of clicking
- **With shell**: Automate it, go write her paper

---

## What Nelle Needs to Learn

1. Navigate to files/directories
2. Create files and directories
3. Check file lengths
4. Chain commands together
5. Retrieve sets of files
6. Iterate over files
7. Run shell scripts

---

<!-- _class: episode-header -->
# Episode 2
## Navigating Files and Directories

---

## Key Navigation Commands

| Command | What it does |
|---------|-------------|
| `pwd`   | **P**rint **W**orking **D**irectory |
| `ls`    | **L**i**s**t contents |
| `cd`    | **C**hange **D**irectory |

```bash
$ pwd
/Users/nelle
```

---

## The File System Tree

```
/
├── bin/
├── data/
├── Users/
│   ├── imhotep/
│   ├── larry/
│   └── nelle/
│       ├── Desktop/
│       ├── Documents/
│       └── Downloads/
└── tmp/
```

- `/` = **root directory** (top of the tree)
- `/Users/nelle` = Nelle's **home directory**

---

## `ls` Options

```bash
$ ls -F          # classify: / for dirs, * for executables
$ ls -l          # long format: details (size, date, permissions)
$ ls -lh         # human-readable sizes (5.3K instead of 5369)
$ ls -a          # show all (including hidden files starting with .)
$ ls -t          # sort by time
$ ls -r          # reverse order
$ ls -lrt        # combine: long, reverse, by time
```

---

## Getting Help

Two ways to learn about commands:

```bash
$ ls --help     # built-in help (Linux, Git Bash)
$ man ls        # manual page (Linux, macOS)
```

- `man` pages: navigate with ↑↓ or Space/b, search with `/`, quit with `q`
- For shell built-ins (like `cd`): use `help cd`

---

## Exploring Other Directories

```bash
$ ls -F Desktop                  # list a different directory
$ cd Desktop/shell-lesson-data   # change to a subdirectory
$ cd ..                          # go up one level
$ cd                             # go home
$ cd ~                           # home directory shortcut
$ cd -                           # previous directory
```

---

## Absolute vs Relative Paths

| Type | Example | Meaning |
|------|---------|---------|
| **Absolute** | `/Users/nelle/Desktop` | From root `/` |
| **Relative** | `Desktop` | From current directory |
| **Relative** | `..` | Parent directory |
| **Shortcut** | `~` | Home directory |
| **Shortcut** | `.` | Current directory |

---

## Tab Completion

Type the first few characters and press **Tab**:

```bash
$ ls nor<Tab>
$ ls north-pacific-gyre/
```

- Saves typing
- Reduces typos
- Press Tab twice to see all possibilities

---

## Shell Command Syntax

```
$ ls -F /
  │  │  │
  │  │  └── Argument (what to operate on)
  │  └───── Option (changes behavior)
  └──────── Command (the program)
```

- **Command** + **Options** (flags) + **Arguments**
- Options: short (`-F`) or long (`--classify`)
- Separated by **spaces** — capitalization matters

---

<!-- _class: episode-header -->
# Episode 3
## Working With Files and Directories

---

## Creating Directories

```bash
$ mkdir thesis                   # create a directory
$ mkdir -p project/data/raw      # create nested directories
```

- `mkdir` = **make directory**
- `-p` = create parent directories as needed
- No output on success (that's normal!)

---

## Creating Files

```bash
$ nano draft.txt     # open text editor
$ touch my_file.txt  # create empty file
```

- `nano` — simple text editor
  - `Ctrl+O` — save (WriteOut)
  - `Ctrl+X` — exit
- `touch` — creates empty file (0 bytes)

---

## Nano Quick Reference

| Keys | Action |
|------|--------|
| `Ctrl+O` | Save file |
| `Ctrl+X` | Exit |
| `Ctrl+G` | Help |
| `Ctrl+K` | Cut line |
| `Ctrl+U` | Paste |

---

## Moving Files (`mv`)

```bash
$ mv thesis/draft.txt thesis/quotes.txt   # rename
$ mv thesis/quotes.txt .                  # move to current dir
$ mv -i old.txt new.txt                   # prompt before overwrite
```

- `mv` = **move** (also renames)
- First argument = source, second = destination
- ⚠️ **Silently overwrites** existing files — use `-i` for safety

---

## Copying Files (`cp`)

```bash
$ cp quotes.txt thesis/quotations.txt     # copy with new name
$ cp quotes.txt thesis/                   # copy into directory
$ cp -r thesis thesis_backup              # copy entire directory
```

- `cp` = **copy**
- `-r` = **recursive** (required for directories)
- Same overwrite warning as `mv`

---

## Removing Files and Directories

```bash
$ rm quotes.txt                # remove a file
$ rm -r thesis                 # remove directory and contents
$ rm -i thesis_backup/*.txt    # prompt before each removal
```

- ⚠️ **No trash bin** — deletion is permanent!
- `rm` alone won't delete directories
- `rm -r` deletes directories and everything inside
- Use `rm -i` for safety

---

## Wildcards

| Wildcard | Meaning | Example |
|----------|---------|---------|
| `*` | Zero or more characters | `*.txt` → all .txt files |
| `?` | Exactly one character | `?.txt` → a.txt but not ab.txt |

```bash
$ ls *.pdb           # all .pdb files
$ ls *dataset*       # files containing "dataset"
$ ls ?ethane.pdb     # methane.pdb, ethane.pdb
```

- The **shell** expands wildcards before running the command

---

## File Naming Best Practices

- ✅ Use lowercase letters, numbers, `.`, `-`, `_`
- ❌ Don't use spaces (use `-` or `_` instead)
- ❌ Don't start names with `-` (looks like an option)
- ❌ Avoid special characters (`*`, `?`, `~`, etc.)
- If you must use spaces, quote the name: `"my file.txt"`

---

<!-- _class: episode-header -->
# Episode 4
## Pipes and Filters

---

## `wc` — Word Count

```bash
$ wc cubane.pdb
    20   156  1158  cubane.pdb
    │     │     │       │
    │     │     │       └── filename
    │     │     └────────── characters
    │     └──────────────── words
    └────────────────────── lines
```

- `wc -l` — lines only
- `wc -w` — words only
- `wc -m` — characters only

---

## Redirecting Output

```bash
$ wc -l *.pdb > lengths.txt    # redirect to file (overwrite)
$ wc -l *.pdb >> lengths.txt   # append to file
```

| Operator | Action |
|----------|--------|
| `>` | Redirect, **overwrite** file |
| `>>` | Redirect, **append** to file |

---

## Viewing File Contents

```bash
$ cat lengths.txt       # print entire file
$ less lengths.txt      # view page by page
```

- `cat` = con**cat**enate — dumps whole file to screen
- `less` — view one screen at a time
  - `Space` — next page, `b` — back, `q` — quit

---

## `sort` and `head`/`tail`

```bash
$ sort -n lengths.txt        # sort numerically
$ head -n 3 animals.csv      # first 3 lines
$ tail -n 3 animals.csv      # last 3 lines
```

- `sort -n` — numerical sort (not alphabetical)
- `head -n N` — first N lines (default: 10)
- `tail -n N` — last N lines (default: 10)

---

## Pipes — The Power of the Shell

```bash
$ wc -l *.pdb | sort -n | head -n 1
```

The `|` (pipe) connects commands:

```
wc -l *.pdb  →  sort -n  →  head -n 1
   (output)      (input)      (input)
```

- Output of left command becomes input of right command
- No intermediate files needed!

---

## Pipes vs Redirects

```bash
# Save to file, then process
$ wc -l *.pdb > lengths.txt
$ sort -n lengths.txt > sorted.txt
$ head -n 1 sorted.txt

# Same thing with pipes — no files!
$ wc -l *.pdb | sort -n | head -n 1
```

---

## The Unix Philosophy

> "Do one thing, and do it well."

- Write small programs that do one job
- Programs read from **standard input**, write to **standard output**
- Combine them with pipes to solve complex problems
- You can (and should) write your own filters

---

## `cut` and `uniq`

```bash
$ cut -d , -f 2 animals.csv        # extract column 2
$ cut -d , -f 2 animals.csv | sort | uniq    # unique values
$ cut -d , -f 2 animals.csv | sort | uniq -c # count occurrences
```

- `cut -d [delim] -f [field]` — extract columns
- `uniq` — remove adjacent duplicates (usually needs `sort` first!)
- `uniq -c` — count occurrences

---

## Ctrl+C — Escape Hatch

If a command seems stuck (or you forgot to give it a filename):

```bash
$ wc -l
(waiting for input...)
```

Press **Ctrl+C** to cancel and return to the prompt.

---

<!-- _class: episode-header -->
# Episode 5
## Loops

---

## Why Loops?

- Perform the same action on **many files**
- Reduce typing (and typos!)
- Key to **automation** and productivity
- Similar to wildcards and tab completion

---

## For Loop Syntax

```bash
for variable in list_of_items
do
    commands using $variable
done
```

```bash
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>     echo $filename
>     head -n 2 $filename | tail -n 1
> done
```

- `$` changes from prompt to `>` while typing the loop body

---

## How Loops Work

```
List: basilisk.dat  minotaur.dat  unicorn.dat

Iteration 1: filename = basilisk.dat  → run commands
Iteration 2: filename = minotaur.dat  → run commands
Iteration 3: filename = unicorn.dat   → run commands
```

- The **variable** (`filename`) gets each value in turn
- Use `$variable` to access its value
- `${variable}` is equivalent — safer in some contexts

---

## Loops with Wildcards

```bash
$ for datafile in *.pdb
> do
>     echo $datafile
> done
```

- The shell expands `*.pdb` **before** the loop starts
- Works with any pattern: `NENE*A.txt`, `*c*`, etc.

---

## Naming Variables

```bash
# Good names — tell you what it is
for filename in *.dat
for datafile in *.pdb

# Bad names — meaningless or misleading
for x in *.dat
for temperature in *.dat
```

Name variables so the **next person** (including future you) understands them.

---

## Loops for File Operations

```bash
# Copy with prefix
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

This runs:
```
cp basilisk.dat original-basilisk.dat
cp minotaur.dat original-minotaur.dat
cp unicorn.dat original-unicorn.dat
```

---

## Debugging with `echo`

Before running a **potentially destructive** loop, dry-run it:

```bash
$ for filename in *.dat
> do
>     echo "cp $filename original-$filename"
> done
```

```
cp basilisk.dat original-basilisk.dat
cp minotaur.dat original-minotaur.dat
cp unicorn.dat original-unicorn.dat
```

- `echo` shows what *would* happen without actually doing it

---

## Spaces and Special Characters

Avoid spaces in filenames! But if you must:

```bash
$ for filename in "red dragon.dat" "purple unicorn.dat"
> do
>     head -n 100 "$filename" | tail -n 20
> done
```

Quote the variable: `"$filename"` — otherwise the shell splits on spaces.

---

## Overwrite vs Append in Loops

```bash
# BAD — overwrites each time, only last file's content remains
for f in *.pdb; do
    cat $f > all.pdb
done

# GOOD — appends, all content saved
for f in *.pdb; do
    cat $f >> all.pdb
done
```

---

## History Commands

```bash
$ history              # show command history
$ !459                 # re-run command #459
$ !!                   # re-run last command
$ !$                   # last word of last command
$ Ctrl+R               # reverse search through history
$ ↑ / ↓                # scroll through previous commands
```

---

<!-- _class: episode-header -->
# Episode 6
## Shell Scripts

---

## What is a Shell Script?

- A file containing shell commands
- Re-run complex operations with a single command
- Makes your work **faster**, **more accurate**, and **reproducible**
- A shell script is really a **small program**

---

## Creating and Running a Script

```bash
$ nano middle.sh          # create/edit the script
```

Content of `middle.sh`:
```bash
head -n 15 octane.pdb | tail -n 5
```

```bash
$ bash middle.sh          # run the script
```

---

## Command-Line Arguments

```bash
$ bash middle.sh octane.pdb   # $1 = octane.pdb
```

| Variable | Meaning |
|----------|---------|
| `$1` | First argument |
| `$2` | Second argument |
| `$3` | Third argument |
| `$@` | **All** arguments |
| `$#` | Number of arguments |

```bash
# middle.sh — now flexible!
head -n "$2" "$1" | tail -n "$3"
```

---

## Adding Comments

```bash
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
```

- Comments start with `#`
- Explain **what** the script does and **how to use it**
- Your future self will thank you!

---

## Processing Multiple Files with `$@`

```bash
# sorted.sh — sort files by line count
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

```bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

`"$@"` expands to all arguments, properly quoted.

---

## Saving History as a Script

```bash
$ history | tail -n 5 > redo-figure-3.sh
```

Then edit the file to:
1. Remove line numbers
2. Remove the `history` command itself
3. You now have a reproducible record!

---

## Nelle's Final Script

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

Run it:
```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt
```

---

## Debugging Scripts

```bash
$ bash -x do-errors.sh NENE*A.txt NENE*B.txt
```

- `-x` = **debug mode** — prints each command as it executes
- Helps find typos, variable issues, and logic errors

---

<!-- _class: episode-header -->
# Episode 7
## Finding Things

---

## `grep` — Find Text in Files

```bash
$ grep pattern filename
```

```bash
$ grep not haiku.txt
```

```
Is not the true Tao, until
"My Thesis" not found
Today it is not working
```

- **G**lobal **R**egular **E**xpression **P**rint
- Finds lines matching a pattern
- Case-sensitive by default

---

## `grep` Options

| Option | Effect |
|--------|--------|
| `-w` | Match whole words only |
| `-n` | Show line numbers |
| `-i` | Case-insensitive |
| `-v` | Invert match (lines NOT matching) |
| `-r` | Recursive (search in subdirectories) |
| `-c` | Count matching lines |
| `-o` | Show only the matching part |

```bash
$ grep -n -w -i "the" haiku.txt
```

---

## `grep` Examples

```bash
$ grep -w "is not" haiku.txt         # phrase search
$ grep -r "Yesterday" .              # recursive search
$ grep -v "not" haiku.txt            # lines without "not"
$ grep -c "rabbit" animals.csv       # count matches
```

---

## Regular Expressions with `grep -E`

```bash
$ grep -E "^.o" haiku.txt
```

- `^` — start of line
- `.` — any single character
- `-E` — extended regular expressions
- Always **quote** regex patterns to prevent shell expansion

---

## `find` — Find Files

```bash
$ find .                    # find everything from current dir
$ find . -type d            # directories only
$ find . -type f            # files only
$ find . -name "*.txt"      # files matching pattern
```

- Recursive by default
- ⚠️ Quote the pattern: `"*.txt"` not `*.txt`
  - Otherwise the shell expands it before `find` sees it

---

## Command Substitution: `$()`

```bash
$ wc -l $(find . -name "*.txt")
```

What happens:
1. Shell runs `find . -name "*.txt"`
2. Replaces `$(...)` with the output
3. Runs: `wc -l ./a.txt ./b.txt ./c.txt`

Any command's output can be used as arguments to another command!

---

## Combining `find` and `grep`

```bash
$ grep "searching" $(find . -name "*.txt")
```

1. `find` finds all `.txt` files
2. `grep` searches inside those files for "searching"

---

## Text vs Binary Files

- `grep`, `wc`, `head`, etc. work on **text files**
- They may not work well on:
  - Images, PDFs, Word documents
  - Databases, spreadsheets
  - Compiled programs
- Convert to text first, or use specialized tools

---

<!-- _class: episode-header -->
# Summary

---

## Core Commands Cheat Sheet

| Category | Commands |
|----------|----------|
| **Navigation** | `pwd` `ls` `cd` |
| **Files/Dirs** | `mkdir` `touch` `cp` `mv` `rm` `nano` |
| **Viewing** | `cat` `less` `head` `tail` |
| **Processing** | `wc` `sort` `uniq` `cut` |
| **Searching** | `grep` `find` |
| **Automation** | `for` loops, shell scripts |
| **Help** | `man` `--help` `history` |

---

## Key Concepts

1. **Pipes** (`|`) chain commands together
2. **Redirects** (`>`, `>>`) send output to files
3. **Wildcards** (`*`, `?`) match file patterns
4. **Variables** (`$var`, `$1`, `$@`) hold values
5. **Loops** (`for ... do ... done`) repeat commands
6. **Scripts** save commands for reuse and reproducibility

---

<!-- _class: episode-header -->
# Questions?
## Happy Shell-ing! 🐚
