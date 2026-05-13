# UT Python Carpentries Training

Welcome to the Python Software Carpentries training.  Please follow these instructions to set up your environment before the workshop.

### Trainers: Adhitya Bhawiyuga (PhD Candidate at UT-ITC), Leila Iñigo de la Cruz (TU Delft), Néstor DelaPaz-Ruíz (UT-LISA)

## Prerequisites

- Python 3.x installed on your computer
- Internet connection for downloading files
- Terminal (in Linux or MacOS), Powershell (Windows) command Line access

## Installing Python 3.x

### Windows

Python is **not** pre-installed on Windows, so you'll need to install it:

1. **Download Python:**
   - Visit [https://www.python.org/downloads/](https://www.python.org/downloads/)
   - Download the latest Python 3.x installer (Python 3.11 or newer recommended)

2. **Run the Installer:**
   - Double-click the downloaded `.exe` file
   - **Important:** Check the box **"Add Python to PATH"** at the bottom
   - Click "Install Now"

3. **Verify Installation:**
   - Open PowerShell or Command Prompt
   - Run: `python --version`
   - You should see something like `Python 3.11.x`

### macOS and Linux

Python 3 is **already pre-installed** on most modern macOS and Linux systems. To verify, run following command in your Terminal:
```bash
python3 --version
```

If Python 3 is not installed or you need a newer version:
- **macOS:** Download from [python.org](https://www.python.org/downloads/) or use Homebrew: `brew install python@3`
- **Linux:** Use your package manager (e.g., `sudo apt install python3 python3-pip python3-venv` on Ubuntu/Debian)

## Setup Instructions

1. Create a directory called `swc-python`, preferably in your Desktop for easier finding.

2. Download the data and code files using the following links for [code](https://swcarpentry.github.io/python-novice-inflammation/files/code/python-novice-inflammation-code.zip) and [data](https://swcarpentry.github.io/python-novice-inflammation/data/python-novice-inflammation-data.zip).

3. Extract both zip files and move them to `swc-python` 

4. Download the `requirements.txt` from this repository file into your `swc-python` directory. Alternatively, create a `requirements.txt` file with the following content:

    ```
    numpy
    jupyterlab
    matplotlib
    ```

5. Open Terminal/Powershell into `swc-python` directory. Then, create a Python virtual environment:

    ```bash
    python -m venv venv
    ```

6. Activate the virtual environment:

    **On macOS/Linux:**
    ```bash
    source venv/bin/activate
    ```

    **On Windows:**
    ```cmd
    venv\Scripts\activate
    ```

    You should see `(venv)` appear at the beginning of your terminal prompt.

7. Install the required Python packages:

    ```bash
    pip install -r requirements.txt
    ```

8. Launch Jupyter Lab:

    ```bash
    jupyter lab
    ```

    This will open Jupyter Lab in your default web browser. You're now ready to start coding!

## Verification

To verify your setup is correct, ensure:

- [ ] You are in the `swc-python` directory
- [ ] The virtual environment is activated (you see `(venv)` in your prompt)
- [ ] All packages are installed without errors
- [ ] Jupyter Lab opens in your browser

## Troubleshooting

### Python Command Not Found
If `python` doesn't work, try `python3` instead:
```bash
python3 -m venv venv
```

### Permission Issues
If you encounter permission errors during installation, ensure your virtual environment is activated.

### Jupyter Lab Won't Start
Make sure you've installed all packages from requirements.txt and your virtual environment is activated.

## Getting Help

If you encounter any issues during setup, please contact your instructor before the workshop begins.

## Deactivating Virtual Environment

When you're done working, you can deactivate the virtual environment:

```bash
deactivate
```
## Dataset: Arthritis Inflammation Cure

Our imaginary colleague "Dr. Maverick" has invented a new miracle drug that promises to cure arthritis inflammation flare-ups after only 3 weeks since initially taking the medication! 

Naturally, we wish to see the clinical trial data, and after months of asking for the data they have finally provided us with a CSV spreadsheet containing the clinical trial data.

The CSV file contains **the number of inflammation flare-ups per day** for the **60 patients** in the initial clinical trial, with the trial lasting **40 days**.

**Each row corresponds to a patient, and each column corresponds to a day in the trial.** Once a patient has their first inflammation flare-up they take the medication and wait a few weeks for it to take effect and reduce flare-ups.

To see how effective the treatment is we would like to:
- Calculate the average inflammation per day across all patients.
- Plot the result to discuss and share with colleagues.

![](https://swcarpentry.github.io/python-novice-inflammation/fig/lesson-overview.svg)

### Data Format

The data sets are stored in comma-separated values (CSV) format:
- each row holds information for a single patient,
- columns represent successive days.

The first three rows of our first file look like this:
```
0,0,1,3,1,2,4,7,8,3,3,3,10,5,7,4,7,7,12,18,6,13,11,11,7,7,4,6,8,8,4,4,5,7,3,4,2,3,0,0
0,1,2,1,2,1,3,2,2,6,10,11,5,9,4,4,7,16,8,6,18,4,12,5,12,7,11,5,11,3,3,5,4,4,5,5,1,1,0,1
0,1,1,3,3,2,6,2,5,9,5,7,4,5,4,15,5,11,9,10,19,14,12,17,7,12,11,7,4,2,10,5,4,2,2,3,2,2,1,1
```
- Each number represents the number of inflammation bouts that a particular patient experienced on a given day. 
- For example, value `6` at row `3` column `7` of the data set above means that the third patient was experiencing inflammation six times on the seventh day of the clinical study.
