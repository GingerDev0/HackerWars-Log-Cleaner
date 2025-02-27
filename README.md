# HackerWars Log Cleaner

A Tampermonkey userscript designed to automatically clear your logs on HackerWars if your IP is detected, while dynamically handling various alerts to ensure a smooth workflow.

## Overview

**HackerWars Log Cleaner (Dynamic IP)** checks HackerWars logs for your current IP address. If it finds a match, the script clears the logs, inserts a custom message into the log textarea, and then triggers the log update process. Additionally, it monitors for success or error alerts and takes appropriate actions—redirecting you or simulating a login click—ensuring a seamless workflow. A new feature now parses IP addresses from the logs (ignoring duplicates and your own IP) and provides a modal for viewing and editing these IPs.

## Features

- **Dynamic IP Detection:**  
  Retrieves your current IP address from the page header.

- **Automated Log Clearance & Custom Insertion:**  
  When your IP is found in the logs, the script clears the log textarea and inserts a custom log message (set by the user) before clicking the "Edit log file" button.

- **Custom Log Message Modal:**  
  Users can set and save a custom log message via a Bootstrap 2.2 modal. The message is stored in localStorage and will be automatically inserted into the log file during clearance.

- **IP Parsing from Logs:**  
  On the logs page, the script extracts IP addresses from log entries formatted like:  
  `2025-02-27 20:38 - [XXX.XXX.XXX.XXX] downloaded file Decent Anti-Virus.av (2.0) at localhost`  
  It removes duplicates and ignores your own IP.

- **Parsed IPs Modal:**  
  A new modal is available to view and edit the list of parsed IP addresses. This list is saved in localStorage as a JSON array.

- **Alert Monitoring:**  
  Listens for specific alert messages to trigger:
  - Redirects after a successful log edit or software download.
  - Login attempts if duplicate IP errors or password cracked messages are detected.
  - Redirects to the log page on software installation/uninstallation alerts.

- **Status Dropdown Menu with Auto-Clear Toggle:**  
  The status container integrated into the site's navigation now features a dropdown menu with options to:
  - Toggle the auto log clearing feature on or off.
  - Open the modal to set a custom log message.
  - Open the modal to view/edit the parsed IP addresses.
  
- **Real-Time Status Updates:**  
  Displays dynamic status messages on the page to keep you informed of each action.

## Installation

1. **Install Tampermonkey:**  
   If you haven't already, install the [Tampermonkey extension](https://www.tampermonkey.net/) for your browser.

2. **Add the Script:**  
   - Open the Tampermonkey dashboard.
   - Click the **+** button to create a new script.
   - Paste the entire script (provided in your userscript file) into the editor.
   - Save the script.

3. **Script Matching:**  
   The script runs on all pages under `https://hackerwars.io/*`.

## How It Works

1. **Initialization:**  
   - The script waits for the page to load and creates a status container that integrates into the site's navigation. This container now includes a dropdown menu with options to toggle auto log clearing, open the custom log message modal, and open the parsed IPs modal.

2. **IP Retrieval:**  
   - It searches for an element with the class `.header-ip-show` to extract your current IP address.

3. **Log Checking & Custom Insertion:**  
   - If on the `/log` page, the script checks if the log textarea contains any text.
   - If your IP is detected in the logs (or on the log page), the script clears the textarea, inserts your saved custom log message, and then clicks the "Edit log file" button to update the logs.

4. **IP Parsing:**  
   - On the logs page (`view=logs`), the script parses IP addresses from the log entries using a regular expression that targets IPs enclosed in square brackets.
   - Duplicate IPs are removed and your own IP is filtered out.
   - The resulting list of IP addresses is saved in localStorage.

5. **Alert Monitoring:**  
   - The script listens for DOM changes to detect alerts.
   - Depending on the alert text, it will either redirect you to a new page or simulate a login button click.

## Usage

Once installed, the script automatically executes on any page under `https://hackerwars.io/*`. Use the "Status" dropdown in the navigation to:
- Monitor updates regarding log clearance, alert handling, and IP parsing.
- Toggle the auto log clearing feature on or off.
- Open the modal to set or update your custom log message.
- Open the modal to view and edit the parsed IP addresses.

## Troubleshooting

- **IP Not Detected:**  
  Ensure the element with class `.header-ip-show` exists on the page. If not, verify that the page layout hasn't changed.

- **Missing Log Area:**  
  If the script logs "Log area element not found," check that you're on the correct page where logs are displayed.

- **IP Parsing Issues:**  
  - Verify that log entries follow the expected format (e.g., `[205.135.68.189]`).
  - Check the browser console for debugging logs related to IP extraction.
  - Confirm that localStorage is updating with the `savedIPs` key.

- **Alert Handling Issues:**  
  If redirection or login actions are not occurring as expected, inspect your browser's console for error messages and confirm that the site's DOM matches the selectors used in the script.

## Customization

- **Styling:**  
  You can customize the appearance of the status container, dropdown menu, and modals by modifying the relevant sections in the script.

- **Alert Conditions:**  
  The script uses text matching to determine actions. If HackerWars updates its alert messages, update the text conditions in the `handleAlert` function accordingly.

- **Custom Log Message:**  
  Update the custom log message via the modal. The message is saved in localStorage and automatically inserted into the log file when logs are cleared.

- **Parsed IPs List:**  
  You can view and edit the parsed IP addresses through the new modal. The list is maintained in localStorage and reflects the unique IP addresses extracted from the logs (excluding your own).

## License

This script is provided as-is without any warranty. You are free to modify and distribute it under your preferred open-source license.
