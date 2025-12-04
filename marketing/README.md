# Marketing Automation Workflows

This directory contains workflows designed to automate your marketing efforts.

## Workflows

*   **[Gmail Campaign](./gmail-campaign.json)**: This workflow allows you to send personalized email campaigns using Gmail and Google Sheets. It tracks email opens and sends follow-up emails automatically.
*   **[Social Media Cross-Posting](./social-media.json)**: This workflow posts a message to multiple social media platforms simultaneously. It's pre-configured for Facebook, Twitter, and LinkedIn.

## Getting Started

1.  **Gmail Campaign**:
    *   Open the `gmail-campaign.json` workflow in n8n.
    *   Follow the instructions in the "Try me out" sticky note to configure the workflow.
    *   You will need to create a Google Sheet with your contact list and connect your Gmail account.

2.  **Social Media Cross-Posting**:
    *   Open the `social-media.json` workflow in n8n.
    *   Replace the placeholder credential IDs with your own credentials for Facebook, Twitter, and LinkedIn.
    *   Customize the message in the nodes.
    *   Activate the workflow to start cross-posting.

## Customization

Feel free to customize these workflows to fit your specific needs. You can add or remove social media platforms, modify the email sequences, and integrate with other services.
