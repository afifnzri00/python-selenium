# firmware-flash-automation

A Python desktop application that automates end-to-end firmware programming for electronic devices - including bootloader upload, serial number injection, firmware flashing, and post-flash verification.

## Overview

This tool was built to eliminate repetitive manual steps involved in programming and configuring hardware devices. It combines serial communication, browser automation, and subprocess control to handle up to 8 devices sequentially in a single batch with real-time status feedback.

## Features

- **Bootloader Upload** - Automatically flashes bootloader via batch script using STM32 ST-LINK Utility
- **Serial Number Injection** - Inputs and verifies device serial numbers through the device web interface using Selenium
- **Firmware Upload** - Uploads firmware file directly through the device browser interface
- **Post-Flash Verification** - Reads back serial number from device config and compares against expected value
- **Real-time Status Indicators** - Green/red LED indicators per device showing bootloader and serial number verification status
- **Batch Processing** - Supports up to 8 devices processed sequentially in one run
- **Serial Port Management** - Connect and disconnect COM ports directly from the GUI

## Tech Stack

- `PyQt6` - Desktop GUI with multithreading support
- `selenium` - Browser automation for device web interface
- `pyserial` - Serial communication with hardware multiplexer
- `subprocess` - Batch script execution for bootloader programming
- `socket` - Device readiness detection after reboot

## Requirements

- Python 3.x
- [STM32 ST-LINK Utility](https://www.st.com/en/development-tools/stsw-link004.html) - required for `flash.bat` bootloader programming
- Chrome for Testing + matching ChromeDriver - no automatic driver updates needed

## Setup

**1. Create a virtual environment:**

```bash
python -m venv .venv
.venv\Scripts\activate
```

**2. Install dependencies:**

```bash
pip install -r requirements.txt
```

**3. Update the file paths in the code to match your machine:**

```python
bat_file = r"YOUR_PATH\flash.bat"
driver_path = r"YOUR_PATH\chromedriver.exe"
chromefortestbinary_path = r"YOUR_PATH\chrome.exe"
```

**4. Run the application:**

```bash
python gui_10_colorbutton.py
```

## Network Requirements

| Device | IP Address |
|---|---|
| Target Device | 192.168.0.100 |

## How It Works

1. Enter serial numbers for each device (up to 8)
2. Select bootloader and firmware files
3. Connect to the COM port of the hardware multiplexer
4. Click **Upload** - the tool will automatically:
   - Flash the bootloader
   - Wait for the device web server to come online
   - Open the device web interface via browser
   - Inject the serial number
   - Upload the firmware
   - Verify the serial number matches after reboot
