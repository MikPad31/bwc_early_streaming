# BWC Early Streaming Iteration 7

- [BWC Early Streaming Iteration 7](#bwc-early-streaming-iteration-7)
  - [Background](#background)
  - [Data](#data)
  - [Setup](#setup)

## Background

Iteration 6 and all past iterations only considered data points from trainees that have passed BWC. Data points from trainees that did not pass BWC were NOT considered. The model from iteration 6 achieved extremely poor performance as a result.

Iteration 7 hence includes data points from all BWC trainees, regardless of whether they passed or failed.

## Data

Refer to [README_DATA.md](docs/README_DATA.md) for more detailed information.

## Setup

This section details how to set up your Python virtual environment using `venv` and how to download and install the necessary Python packages using `pip`. My Python version is `Python 3.12.3` but any other Python version should work as long as `scikit-learn` supports it.

1. In this project's root folder, open a terminal.
2. Run the following commands:

- i. To create a virtual environment using `venv`:

   ```bash
   # If you are on Windows:
   python -m venv .venv

   # If you are on MacOS/Linux/WSL2:
   # you might need to run sudo apt install python python3-pip python3-venv
   python3 -m venv .venv
   ```

- ii. To activate the virtual environment:

   ```bash
   # If you are on Windows:
   .venv\Scripts\activate

   # If you are on MacOS/Linux/WSL2:
   source .venv/bin/activate
   ```

- iii. To download and install the required packages:

   ```bash
   python -m pip install --upgrade pip  # Upgrade pip if necessary
   pip install -r requirements.txt
   ```

Ensure that you have activated your virtual environment before running any code in the notebooks.
