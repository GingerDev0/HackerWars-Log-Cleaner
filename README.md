# HackerWars QOL Script

A Tampermonkey userscript designed to improve your HackerWars experience by automatically clearing your logs when your IP is detected, inserting a custom log message, and parsing valuable information from your logs—such as IP addresses, BTC addresses, and bank account details—while dynamically handling alerts for a smooth workflow.

## Overview

**HackerWars QOL Script** monitors your HackerWars logs to detect your current IP address. When your IP is found, the script clears the logs, inserts a custom log message, and triggers the log update process. In addition, it extracts useful information from your logs:
- **IP addresses:** Parses IPs (ignoring duplicates and your own IP).
- **BTC addresses:** Captures account and key information.
- **Bank accounts:** Extracts bank account numbers and bank IPs.

All parsed data is stored persistently in localStorage and can be viewed and edited via user-friendly modals. The script also monitors alerts and takes appropriate actions, such as redirecting you or simulating a login click, ensuring a seamless experience.

## Features

- **Dynamic IP Detection:**  
  Retrieves your current IP address from the page header.

- **Automated Log Clearance & Custom Insertion:**  
  When your IP is detected in the logs, the script clears the log textarea and inserts a custom log message (set by you) before clicking the "Edit log file" button.

- **Custom Log Message Modal:**  
  Set and save a custom log message via a Bootstrap modal. This message is stored in localStorage and automatically inserted when logs are cleared.

- **IP Parsing from Logs:**  
  Parses IP addresses from log entries formatted like:  
  `2025-02-27 20:38 - [XXX.XXX.XXX.XXX] downloaded file Decent Anti-Virus.av (2.0) at localhost`  
  It removes duplicates and excludes your own IP.

- **BTC Address Parsing:**  
  Extracts BTC address details from log lines such as:  
  `2025-02-27 20:46 - localhost logged in to [XXX.XXX.XXX.XXX] on account r4IUAo7OchzL6d2nrf0Kg3O4CGpdWV9Qkx using key CjizhbCYHW64509iPddWOw46ipt3zCoZYNg8i06MggKVIzt2deJCzKyiQ7HFmTHq`  
  The script captures both the account and the key, merging new entries with previously stored data.

- **Bank Account Parsing:**  
  Extracts bank account information from logs formatted like:  
  `2025-02-27 20:47 - localhost logged on account #XXXXXXXXX on bank [XXX.XXX.XXX.XXX]`  
  It captures the account number and bank IP, and persists this data in localStorage.

- **Parsed Data Modals:**  
  Separate modals allow you to view and edit the parsed IP addresses, BTC addresses, and bank accounts.

- **Alert Monitoring:**  
  Monitors specific alert messages to trigger:
  - Redirects after a successful log edit or software download.
  - Login attempts if duplicate IP errors or password cracked messages are detected.
  - Redirects to the log page on software installation/uninstallation alerts.

- **Status Dropdown Menu with Auto-Clear Toggle:**  
  Integrated into the site's navigation, the status container features a dropdown menu with options to:
  - Toggle the auto log clearing feature.
  - Open the modal to set a custom log message.
  - Open the modals to view/edit parsed IP addresses, BTC addresses, and bank accounts.

- **Real-Time Status Updates:**  
  Displays dynamic status messages on the page to keep you informed of each action.

## Installation

1. **Install Tampermonkey:**  
   If you haven't already, install the [Tampermonkey extension](https://www.tampermonkey.net/) for your browser.

2. **Add the Script:**  
   - Open the Tampermonkey dashboard.
   - Click the **+** button to create a new script.
   - Paste the entire script (provided in the userscript file) into the editor.
   - Save the script.

3. **Script Matching:**  
   The script runs on all pages under `https://hackerwars.io/*`.

## How It Works

1. **Initialization:**  
   - The script waits for the page to load and creates a status container integrated into the site's navigation.
   - The dropdown menu offers options to toggle auto log clearing, open the custom log message modal, and access the parsed data modals.

2. **IP Retrieval:**  
   - It extracts your current IP address from the element with the class `.header-ip-show`.

3. **Log Checking & Custom Insertion:**  
   - On the `/log` page (or on `/internet`), the script checks if the log textarea contains any text.
   - When your IP is detected, it clears the textarea, inserts your saved custom log message, and clicks the "Edit log file" button.

4. **Data Parsing:**  
   - **IP Parsing:** Extracts IP addresses from log entries, removes duplicates, and excludes your own IP.
   - **BTC Parsing:** Extracts BTC account and key details from logs.
   - **Bank Parsing:** Extracts bank account numbers and bank IPs.
   - All parsed data is merged with existing entries and stored persistently in localStorage.

5. **Alert Monitoring:**  
   - The script listens for DOM changes to detect alerts.
   - Based on alert text, it may redirect you or simulate a login click.

## Usage

After installation, the script runs automatically on any page under `https://hackerwars.io/*`. Use the "Status" dropdown in the navigation to:
- Monitor updates regarding log clearance, alert handling, and data parsing.
- Toggle the auto log clearing feature.
- Open the modals to set or update your custom log message, or to view/edit parsed IP addresses, BTC addresses, and bank accounts.

## Troubleshooting

- **IP Not Detected:**  
  Ensure the element with the class `.header-ip-show` is present. If not, check for layout changes.

- **Missing Log Area:**  
  If you see a "Log area element not found" message, verify you are on the correct page where logs are displayed.

- **Data Parsing Issues:**  
  - Confirm log entries follow the expected formats (e.g., `[XXX.XXX.XXX.XXX]` for IPs, the proper format for BTC and bank entries).
  - Check the browser console for debugging logs regarding data extraction.
  - Ensure localStorage is updating with keys like `savedIPs`, `savedBTC`, and `savedBank`.

- **Alert Handling Issues:**  
  If expected actions (redirects or login simulations) are not occurring, inspect the browser console for errors and verify that the site's DOM matches the script's selectors.

## Customization

- **Styling:**  
  Modify the script sections for the status container, dropdown menu, and modals to adjust their appearance.

- **Alert Conditions:**  
  Update the text conditions in the alert handling function if HackerWars changes its alert messages.

- **Custom Log Message:**  
  Set or update your custom log message via the modal. This message is saved in localStorage and automatically inserted during log clearance.

- **Parsed Data Lists:**  
  View and edit the parsed IP addresses, BTC addresses, and bank accounts through their respective modals. The lists are stored as JSON in localStorage and merged with new entries as they are parsed.

## License

This script is provided as-is without any warranty. You are free to modify and distribute it under your preferred open-source license.
