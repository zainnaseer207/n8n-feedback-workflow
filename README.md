# n8n Feedback Agent

An n8n automation that collects customer feedback, uses Google Gemini to classify it, stores the feedback in Airtable, sends Slack notifications, and emails the customer when the feedback is classified as a complaint.

## Workflow

```text
Customer
   |
   v
Feedback Form
   |
   +--------------------+
   |                    |
   v                    v
AI Agent           Original Form Data
   |                    |
   +---------+----------+
             |
             v
           Merge
             |
             v
           Switch
        /     |      \
       /      |       \
      v       v        v
 Complaint Compliment Feature Addition
      |       |        |
      v       v        v
   Airtable Airtable Airtable
      |
      v
     Slack
      |
      v
     Gmail
```

## Workflow Preview

![Feedback Agent Workflow](screenshots/01-feedback-form.png)

## AI Classification

![AI Agent](screenshots/02-ai-agent.png)

## Routing

![Switch Routing](screenshots/03-switch-routing.png)

## Airtable

![Airtable](screenshots/04-airtable.png)

## Notifications

![Gmail](screenshots/06-gmail.png)

## What the workflow does

1. Collects **Name**, **Email**, **Phone number**, and **Feedback** through an n8n form.
2. Sends the feedback to a Google Gemini-powered AI Agent.
3. Classifies feedback as:
   - `Complain`
   - `Compliment`
   - `Feature addition`
4. Uses a Switch node to route the result.
5. Creates an Airtable record for each category.
6. Sends a Slack notification for complaint and feature-update routes.
7. Sends an email to the customer on the complaint route.

## Repository structure

```text
n8n-feedback-agent/
├── workflows/
│   └── feedback-agent.json
├── docs/
│   ├── setup.md
│   └── security.md
├── screenshots/
│   └── .gitkeep
├── .gitignore
└── README.md
```

## Requirements

- n8n
- Google Gemini credential
- Airtable credential
- Slack OAuth credential
- Gmail OAuth credential

## Import

1. Open your n8n instance.
2. Go to **Workflows**.
3. Choose **Import from File**.
4. Select `workflows/feedback-agent.json`.
5. Configure the credentials used by the workflow.
6. Verify the Airtable base/table and Slack channels.
7. Test each route before activating the workflow.

## Security

This repository intentionally does **not** contain live API keys, OAuth tokens, passwords, or n8n instance metadata.

Credentials must be configured inside n8n.

Do not commit `.env` files, API keys, OAuth tokens, passwords, or private customer feedback data.

## Important implementation note

The current workflow's three Airtable branches point to the same Airtable base/table configuration. If you want separate tables for complaints, compliments, and feature requests, update those Airtable nodes before production use.

The current workflow also sends a fixed complaint email body. For production use, consider replacing it with a shorter dynamic acknowledgement that uses the customer's actual feedback and avoids hard-coded wording.

## Development

Recommended commit messages:

```text
feat: add feedback classification workflow
fix: improve complaint routing
feat: add Slack notification
feat: add complaint email acknowledgement
docs: update setup instructions
security: sanitize exported workflow credentials
```

## License

Choose a license appropriate for your project before publishing publicly.
