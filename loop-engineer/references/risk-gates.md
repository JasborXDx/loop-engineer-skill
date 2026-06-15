# Risk Gates

Use risk gates to decide when an AI loop can act automatically and when it must pause for human confirmation.

## Low Risk

Usually safe to automate after the objective is clear:

- Reading public webpages
- Summarizing sources
- Creating draft files
- Running local tests
- Generating local reports
- Sorting or deduplicating non-sensitive data
- Taking screenshots for inspection

## Medium Risk

Can often be automated, but verify before finalizing:

- Editing local project files
- Opening logged-in pages
- Filling draft forms without submitting
- Creating draft emails or messages
- Updating non-public reports
- Calling paid APIs with small, bounded cost
- Uploading non-sensitive files to user-approved targets

Add a clear confirmation step before irreversible or external effects.

## High Risk

Always require explicit confirmation immediately before action:

- Submitting forms, applications, bug reports, or platform tasks
- Sending emails, DMs, support tickets, or public comments
- Publishing posts, listings, videos, or reviews
- Changing account profile, identity, payment, privacy, or security settings
- Buying, selling, refunding, transferring, or using bank/card/crypto/payment data
- Deleting, overwriting, or mass-updating data
- Uploading identity documents, contracts, private photos, credentials, or secrets
- Accepting terms, legal agreements, NDAs, or employment/project commitments

## Prohibited or Stop-and-Ask Cases

Stop rather than automate when the request requires:

- Bypassing captchas, anti-bot systems, platform access controls, or account restrictions
- Misrepresenting identity, location, qualifications, ownership, or device access
- Hidden scraping against a platform's clear restrictions
- Submitting false testing results, fake bug reports, fake reviews, or fake credentials
- Handling credentials in chat or exposing secrets to external tools

## Confirmation Wording

Use direct confirmation prompts:

```text
I have filled the draft. Before I submit, confirm that you want me to click Submit.
```

```text
This will change your account profile. Confirm that I should save these changes.
```

```text
This may spend money or use payment details. I will not continue without explicit confirmation.
```
