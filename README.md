# X-Plane 12 US FAA CIFP Updater

A simple Python script to download the latest US FAA CIFP (Coded Instrument Flight Procedures) navigation data and install it as `earth_424.dat` for X-Plane 12.

**Note:** This script currently only handles **US data** from the FAA CIFP source. It does *not* provide worldwide navigation data.

## Features

*   Automatically fetches the latest FAA CIFP cycle page.
*   Parses the page to find the correct download link and effective dates.
*   Checks if the current date is within the cycle's effective range before downloading.
*   Downloads the data ZIP if needed (with a progress bar via `rich`).
*   Extracts the required data file (`FAACIFP18`).
*   Renames it to `earth_424.dat`.
*   Places it in the X-Plane 12 'Custom Data' folder (overwriting the previous file).
*   Cleans up the downloaded ZIP file.
*   Remembers the X-Plane path after the first successful run (stored in `~/.cifp_updater/config.path`).
*   Provides command-line options (`--set-path`, `--forget-path`) to manage the saved path.
*   Cross-platform compatible (tested on Linux, should work on macOS and Windows).

## Requirements

*   Python 3.6+
*   `pip` (Python package installer)
*   Required Python packages:
    *   `requests`
    *   `rich`
    *   `beautifulsoup4`

## Installation

1.  Clone this repository or download the `cifp_updater.py` script.
2.  Install the required packages. Using a virtual environment is highly recommended:

    ```bash
    # Create a virtual environment (optional but recommended)
    python -m venv venv
    # Activate it (Linux/macOS)
    source venv/bin/activate
    # Activate it (Windows CMD)
    # venv\Scripts\activate.bat
    # Activate it (Windows PowerShell)
    # venv\Scripts\Activate.ps1

    # Install packages
    pip install requests rich beautifulsoup4
    ```
    Alternatively, if using a system package manager like `pacman` (Arch/Manjaro/CachyOS):
    ```bash
    sudo pacman -S python-requests python-rich python-beautifulsoup4
    ```

## Usage

1.  Navigate to the script's directory in your terminal.
2.  Run the script:
    ```bash
    python cifp_updater.py
    ```
3.  The first time you run it (or after using `--forget-path`), it will prompt for the full path to your X-Plane 12 installation directory.
4.  On subsequent runs, it will automatically use the saved path.

### Command-Line Options

*   `python cifp_updater.py -h`: Show the help message and usage options.
*   `python cifp_updater.py --set-path /path/to/your/XPlane12`: Set or update the saved X-Plane path. The script will validate the path, save it, and then proceed with the update check using this path.
*   `python cifp_updater.py --forget-path`: Remove the saved path. The script will then prompt you for the path on this run.

## Disclaimer

This script relies on web scraping the FAA website structure. **Changes made by the FAA to their website layout may break the script's functionality**, so I may need to update the parsing logic if the website changes.

![CIFP Updater Example Output](assets/CIFP_Updater.png)
