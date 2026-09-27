# Security Guide

## Never commit

Do not commit:

- API keys
- OAuth access/refresh tokens
- Passwords
- Webhook secrets
- Private customer information
- `.env` files
- Production database credentials
- Private n8n instance metadata

## Credentials

Keep credentials in n8n's credential manager rather than embedding secrets in workflow JSON.

## Public GitHub repository

Before making this repository public:

1. Search the repository for `apiKey`, `token`, `password`, `secret`, and `Authorization`.
2. Review the workflow JSON manually.
3. Confirm that no customer feedback, names, emails, or phone numbers are present as sample data.
4. Review Git history, not just the latest files. A secret committed in an earlier commit can remain accessible in Git history.
5. If a real secret was ever committed, rotate/revoke it rather than merely deleting it from the latest file.

## Customer data

Feedback may contain personal information. Do not place real customer submissions in screenshots, README examples, test fixtures, or public GitHub issues.
