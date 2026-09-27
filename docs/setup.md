# Setup Guide

## 1. Import the workflow

Import:

`workflows/feedback-agent.json`

into n8n.

## 2. Configure Google Gemini

The AI Agent requires a Google Gemini chat model. Create/select your Gemini credential in n8n and assign it to the **Google Gemini Chat Model** node.

The classifier is instructed to return one of exactly three labels:

- `Complain`
- `Compliment`
- `Feature addition`

## 3. Configure Airtable

The workflow uses Airtable create-record nodes.

Verify:

- Base
- Table
- Name field
- Email field
- Phone number field
- Feedback field

The original workflow routes all three categories to the same Airtable base/table configuration. Change this if separate storage is required.

## 4. Configure Slack

The workflow has Slack notification nodes.

Verify the destination channels and connect your Slack OAuth credential.

## 5. Configure Gmail

The complaint route sends an email to:

`{{ $('Merge').item.json.Email }}`

Connect the Gmail OAuth credential and review the subject/body before production use.

## 6. Test

Submit at least one example for each category:

### Complaint
> The service was delayed and I am unhappy with the experience.

### Compliment
> Your support team was very helpful and professional.

### Feature addition
> Please add an option to export reports as PDF.

Confirm that:

- Gemini returns the expected label.
- The Switch routes correctly.
- Airtable receives the record.
- Slack receives the expected notification.
- Complaint emails are sent only on the complaint route.

## 7. Activate

Only activate the workflow after all three paths have been tested successfully.
