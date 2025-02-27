# HackerWars Log Cleaner

A Tampermonkey userscript designed to automatically clear your logs on HackerWars if your IP is detected, while dynamically handling various alerts to ensure a smooth workflow.

## Overview

**HackerWars Log Cleaner (Dynamic IP)** checks HackerWars logs for your current IP address. If it finds a match, the script clears the logs and monitors for success or error alerts. Depending on the alert detected, the script will redirect you to the appropriate page or simulate a click on the login button. This automation helps keep your logs clean and your workflow uninterrupted.

## Features

- **Dynamic IP Detection:**  
  Retrieves your current IP address from the page header.
  
- **Automated Log Clearance:**  
  Clears logs either unconditionally on the log page or when your IP is found in the logs.
  
- **Alert Monitoring:**  
  Listens for specific alert messages to trigger:
  - Redirects after a successful log edit or software download.
  - Login attempts if duplicate IP errors or password cracked messages are detected.
  - Redirects to the log page on software installation/uninstallation alerts.
  
- **Status Dropdown Menu with Auto-Clear Toggle:**  
  The status container in the navigation now features a dropdown menu. Clicking on the "Status" button reveals the dropdown, which contains the auto log clearing toggle. You can easily turn auto log clearing on or off, with your preference saved via localStorage for persistence across sessions.
  
- **Status Updates:**  
  Displays real-time status messages on the page using a dynamically created status container.

## Installation

1. **Install Tampermonkey:**  
   If you haven't already, install the [Tampermonkey extension](https://www.tampermonkey.net/) for your browser.

2. **Add the Script:**  
   - Open the Tampermonkey dashboard.
   - Click the **+** button to create a new script.
   - Paste the entire script (provided below) into the editor.
   - Save the script.

3. **Script Matching:**  
   The script runs on all pages under `https://hackerwars.io/*`.

## How It Works

1. **Initialization:**  
   - The script creates a status container integrated into the site's navigation. This container now includes a dropdown menu that holds the auto log clearing toggle option.
   
2. **IP Retrieval:**  
   - It searches for an element with the class `.header-ip-show` to extract your current IP address.

3. **Log Checking:**  
   - If on the `/log` page, the logs are cleared immediately.
   - Otherwise, the script checks the log area for your IP and clears the logs if found.

4. **Alert Monitoring:**  
   - The script listens for changes in the DOM to detect alerts.
   - Depending on the alert text, it will either redirect you to a new page or simulate a login click.

## Usage

Once installed, the script automatically executes on any page under `https://hackerwars.io/*`. Use the "Status" dropdown in the navigation to:
- Monitor updates regarding log clearance and alert handling.
- Toggle the auto log clearing feature on or off as needed.

## Troubleshooting

- **IP Not Detected:**  
  Ensure the element with class `.header-ip-show` exists on the page. If not, verify that the page layout hasn't changed.

- **Missing Log Area:**  
  If the script logs "Log area element not found," check that you're on the correct page where logs are displayed.

- **Alert Handling Issues:**  
  If redirection or login actions are not occurring as expected, inspect your browser's console for error messages and confirm that the site's DOM matches the selectors used in the script.

## Customization

- **Styling:**  
  You can customize the appearance of the status container and dropdown menu by modifying the relevant sections in the script.

- **Alert Conditions:**  
  The script uses text matching to determine actions. If HackerWars updates its alert messages, update the text conditions in the `handleAlert` function accordingly.

## License

This script is provided as-is without any warranty. You are free to modify and distribute it under your preferred open-source license.
