# UT Unix Shell Carpentries Training

This repository contains training materials for the **UT Unix Shell Carpentries Training**, based on [Software Carpentries: The Unix Shell](https://swcarpentry.github.io/shell-novice/).

## Content

The training covers the following episodes:

1. **Introducing the Shell** — What is the shell, why use it, and your first commands
2. **Navigating Files and Directories** — `pwd`, `ls`, `cd`, absolute vs. relative paths, tab completion
3. **Working With Files and Directories** — `mkdir`, `cp`, `mv`, `rm`, wildcards, and file naming practices
4. **Pipes and Filters** — Combining commands with `|`, redirection (`>`, `>>`), and filter commands
5. **Loops** — Automating repetitive tasks with `for` loops
6. **Shell Scripts** — Writing reusable scripts with arguments and comments
7. **Finding Things** — Using `grep` and `find` to locate text and files

## Setup

Follow these steps to prepare for the workshop.

### 1. Download Files

1. Download [**shell-lesson-data.zip**](https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip) and move the file to your Desktop.
2. Unzip/extract the file. You should end up with a new folder called **`shell-lesson-data`** on your Desktop.

> **Note:** In some cases, the extracted zip folder may be duplicated, so you might have a folder `shell-lesson-data` containing another folder with the same name. On Windows, this happens when double-clicking the zip file. To avoid this, right-click the zip file and choose "Extract All…" instead.

### 2. Install Software

If you do not already have a Unix shell installed, follow the [Carpentries installation instructions for the shell](https://carpentries.github.io/workshop-template/install_instructions/#shell).

- **Windows:** Install [Git for Windows](https://carpentries.github.io/workshop-template/install_instructions/#shell), which includes Git Bash. Open Git Bash from the Start menu. Advanced users may alternatively use the [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).
- **macOS:** Open the **Terminal** application from the Utilities folder (or search for it with Spotlight). The default shell on macOS Catalina and later is Zsh; on earlier versions it is Bash. If needed, type `bash` in the terminal to run Bash.
- **Linux:** Open a terminal (e.g., Gnome Terminal, KDE Konsole, or xterm) from the applications menu or search bar. The default shell is usually Bash.

### 3. Open a New Shell

1. Open your terminal application.
2. Type `cd` and press **Return**. This ensures you start in your home directory.

In the lesson, you will learn how to access the data files in the `shell-lesson-data` folder.

## Slide Deck

The training is presented as a slide deck located in `slides.md`.

### Generating Slides from Markdown

This project uses **[Marp](https://marp.app/)** to generate slides from Markdown.

#### Option 1: VS Code with Marp Extension

1. Install the [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) extension
2. Open `slides.md`
3. Use the preview button or export to HTML/PDF/PPTX via the command palette (`Cmd/Ctrl + Shift + P` → "Marp: Export Slide Deck")

#### Option 2: Marp CLI

Install the Marp CLI globally via npm:

```bash
npm install -g @marp-team/marp-cli
```

Then generate the slides:

```bash
# Export to HTML
marp slides.md -o slides.html

# Export to PDF
marp slides.md --pdf -o slides.pdf

# Export to PowerPoint
marp slides.md --pptx -o slides.pptx

# Start a live preview server
marp --watch --preview slides.md
```

#### Option 3: Docker

```bash
docker run --rm -v $PWD:/home/marp/app/ -e MARP_USER=$(id -u):$(id -g) marpteam/marp-cli slides.md -o slides.html
```

## License

These materials are based on Software Carpentries lessons and are licensed under [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/).
