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
