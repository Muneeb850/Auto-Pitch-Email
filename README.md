#Auto Pitch Emails (Gemini + File Upload)

An n8n workflow that automates cold outreach emails to dental practices. Upload a business list (Excel/CSV), and the workflow generates a personalized pitch email for each business using Google Gemini, then sends it via Gmail.

## How it works

1. **Upload Business List** — A form trigger accepts an Excel or CSV file containing `Business Name`, `Phone`, `Email`, `Manager`, and `Service Pitch` columns.
2. **Convert Sheet to Data** — Parses the uploaded file into individual rows.
3. **Loop Over Businesses** — Processes each business one at a time.
4. **Wait** — A short delay between iterations to avoid rate limits.
5. **Prepare Data** — Builds a personalized prompt based on whether the business needs an AI Agent pitch or a website pitch (determined by the `Service Pitch` column).
6. **Message a model (Gemini)** — Generates a short, human-sounding cold email using Google Gemini (`gemini-2.5-flash`).
7. **Code in JavaScript** — Cleans up the AI-generated text (removes any accidental sign-offs, converts to HTML paragraphs).
8. **Send Pitch Email** — Sends the finished email via Gmail, with a signature appended.

## Requirements

- An n8n instance (self-hosted or cloud)
- Gmail OAuth2 credentials configured in n8n
- Google Gemini (PaLM) API credentials configured in n8n

## Setup

1. Import `workflow.json` into your n8n instance.
2. Reconnect the **Gmail** and **Google Gemini** credential nodes with your own credentials (these were stripped from this export for security).
3. Update the signature block inside the **Send Pitch Email** node with your own name, phone, and email.
4. Activate the workflow and use the generated form URL to upload your business list.

## Input file format

Your Excel/CSV should include these columns:

| Business Name | Phone | Email | Manager | Service Pitch |
|---|---|---|---|---|

## Notes

- This workflow was built for outreach to dental practices but can be adapted to any industry by editing the prompts in the **Prepare Data** node.
- Credentials, instance IDs, and personal contact info have been removed from this export. You'll need to add your own before running it.
