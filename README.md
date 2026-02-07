# ai-email-agent-n8n
n8n workflow that automates email processing using OpenAI. Classifies emails as Urgent, Invoice, Newsletter, or Spam and triggers actions in Slack and Google Sheets.
# AI Email Classifier & Automator

This n8n workflow automates inbox management by using OpenAI to categorize incoming emails based on their content. Instead of simple keyword matching, it uses an LLM to understand the context of the message and executes specific actions for urgent issues, invoices, newsletters, and spam.

## Workflow Overview

The system performs the following steps:

1.  **Fetch:** Retrieves unread emails from Gmail.
2.  **Analyze:** Sends the email body to OpenAI (GPT-5 Mini) to determine if the message is "Urgent," "Invoice," "Newsletter," or "Spam."
3.  **Route:** A Switch node directs the workflow based on the AI's categorization.
4.  **Action:**
    * **Urgent:** Sends an immediate alert to Slack including the sender and subject.
    * **Invoice:** Extracts key details and appends them to a Google Sheet for finance tracking. It also sends a Slack notification.
    * **Newsletter:** Automatically deletes the email.
    * **Spam:** Automatically deletes the email.

## Tech Stack

* **n8n:** Workflow automation platform.
* **OpenAI API:** Used for text classification (GPT-5 Mini).
* **Gmail API:** For fetching and deleting messages.
* **Slack API:** For sending notifications.
* **Google Sheets API:** For logging structured data.

## Setup Instructions

1.  **Import the Workflow:**
    * Download the `workflow.json` file from this repository.
    * Open your n8n editor.
    * Select "Import from File" and upload the JSON.

2.  **Configure Credentials:**
    You will need to set up credentials in n8n for the following services:
    * Gmail (OAuth2)
    * OpenAI API
    * Slack (OAuth2)
    * Google Sheets (OAuth2)

3.  **Prepare the Google Sheet:**
    Create a new Google Sheet and add the following headers in the first row:
    * Column A: DATE
    * Column B: FORM
    * Column C: SUBJECT
    * Column D: EMAIL-CONTENT

4.  **Customize Settings:**
    * **Gmail Node:** The workflow currently fetches unread emails received after a specific date. You can adjust the filters in the "Get many messages" node.
    * **Slack Node:** Update the "Send Message To" field to select your specific Slack User ID or Channel.
