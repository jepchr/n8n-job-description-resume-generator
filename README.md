# Draft Resume Builder - Text

An n8n workflow that generates a tailored resume from a copy-pasted job description.

## Overview

This workflow accepts job details via a form (title, company, description, optional URL) and generates a customized resume using Claude Opus 4.5. This is a simpler variant of the LinkedIn URL Resume Generator - no scraping required.

## Workflow Flow

```
Form Trigger → ┌───────────────────┬───────────────────┐
               ↓                   ↓                   ↓
       Get Master Resume   Get Prompt Instructions   Copy Resume Template
               ↓                   ↓                   ↓
               └───────────────────┼───────────────────┘
                                   ↓
                         Wait for All Inputs (Merge)
                                   ↓
                         Prepare Claude Input
                                   ↓
                   Generate Resume Content (Claude Opus 4.5)
                                   ↓
                         Parse Claude Response
                                   ↓
                   Update Doc (Replace Placeholders)
                                   ↓
                     Add to Processed Jobs Sheet
```

## Features

- **Form-based input**: Web form with fields for Job Title, Company, Job Description (textarea), and optional URL
- **No scraping required**: Paste job descriptions directly from any source
- **Claude Opus 4.5**: Generates tailored resume content based on job requirements
- **Google Docs integration**: Copies template and replaces placeholders
- **Tracking**: Adds processed jobs to Google Sheets with resume link

## Prerequisites

- n8n instance (tested on n8n 2.0 Cloud)
- Google Workspace credentials (Docs, Drive, Sheets)
- Anthropic API key (for Claude Opus 4.5)

## Form Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| Job Title | Text | Yes | e.g. "Senior Content Marketing Manager" |
| Company | Text | Yes | e.g. "Acme Corp" |
| Job Description | Textarea | Yes | Full job description text |
| Job URL | Text | No | Original posting URL (for tracking) |

## Google Document IDs

| Document | ID |
|----------|-----|
| Master Resume | `1nkYGAspSoYA3lb3lStGdYVkKd7CRFt53OewhOuazADc` |
| Prompt Instructions | `1KMaK8-Wqud1INyw_VHs3XS0TdO4kX-sX5q8_ZUPKvy8` |
| Resume Template | `1pSd0QVcsNy1bfZTe6mvb13YIzpEnOo4E_fpPk7H9SuU` |
| Job Tracking Sheet | `1S5i0OIJxXrMBAziWqiSiy3lyAwgzh_aKlydnrciwUuQ` |

## n8n Cloud Workflow ID

`BfEoJLTqmMQ2wm2k`

## Related Workflows

- [n8n-linkedin-url-resume-generator](https://github.com/jepchr/n8n-linkedin-url-resume-generator) - URL-based variant (scrapes LinkedIn)
- [n8n-resume-generator](https://github.com/jepchr/n8n-resume-generator) - Batch resume generator (processes from Relevant Roles sheet)
- [n8n-linkedin-jobs-email](https://github.com/jepchr/n8n-linkedin-jobs-email) - Gmail-triggered job scraper
- [n8n-linkedin-jobs-web](https://github.com/jepchr/n8n-linkedin-jobs-web) - Scheduled Apify-based scraper
