# AI Social Media Auto-Poster — n8n + GPT-4o-mini

Automatically generates and publishes engaging social media posts to LinkedIn and Twitter/X using AI. Just fill in your content queue in Google Sheets — the bot does the rest, 3 times a week.

## How It Works

```
Schedule → Google Sheets (topic) → GPT-4o-mini → LinkedIn + Twitter/X → Mark as Posted
```

1. Runs automatically Mon, Wed, Fri at 9 AM
2. Reads next pending topic from Google Sheets
3. GPT-4o-mini writes platform-optimized posts
4. Posts to LinkedIn and Twitter/X simultaneously
5. Updates Google Sheets status to "Posted"

## What AI Generates

**LinkedIn post:**
- Professional tone, 150-200 words
- Key insights and takeaways
- Engagement question at the end
- 3-5 relevant hashtags

**Twitter/X post:**
- Punchy hook in first line
- Under 250 characters
- 2-3 hashtags

## Quick Start

### 1. Set Up Google Sheets

Create a sheet named **Content Queue** with these columns:
```
Topic | Industry | Tone | Notes | Status | LinkedIn_Post | Twitter_Post | Posted_At
```

Fill in:
- `Topic` — what to write about (e.g. "AI automation benefits for SMEs")
- `Industry` — your industry (e.g. "Technology", "Real Estate")
- `Tone` — post tone (e.g. "Professional", "Casual", "Inspirational")
- `Notes` — extra context (optional)
- `Status` — set to `Pending`

### 2. Import Workflow
- Go to your n8n instance
- Click **+** → **Import workflow**
- Upload `ai-social-autoposter.json`

### 3. Configure Nodes

**Get Next Topic & Mark as Posted nodes:**
- Add Google Sheets OAuth2 credential
- Replace `YOUR_GOOGLE_SHEET_ID` with your actual Sheet ID

**Generate Posts node:**
- Add OpenAI API key

**Post to LinkedIn node:**
- Add LinkedIn OAuth2 credential
- Replace `YOUR_LINKEDIN_PERSON_ID` with your LinkedIn Person URN

**Post to Twitter/X node:**
- Add Twitter OAuth1 credentials (API Key, API Secret, Access Token, Access Secret)

### 4. Customize Schedule

Default: Mon, Wed, Fri at 9 AM

To change, edit the cron expression in Schedule Trigger:
```
0 9 * * 1,3,5   → Mon, Wed, Fri at 9 AM
0 8 * * 1-5     → Every weekday at 8 AM
0 10 * * 1      → Every Monday at 10 AM
```

### 5. Activate
- Toggle workflow to **Active**
- Add topics to Google Sheets with Status = "Pending"

## Use Cases

- Marketing agencies managing multiple client accounts
- Founders building personal brand on autopilot
- SaaS companies posting thought leadership content
- Consultants staying visible without daily effort
- Any business needing consistent social media presence

## Content Ideas for Google Sheets

| Topic | Industry | Tone |
|-------|----------|------|
| 5 ways AI saves time for small businesses | Technology | Professional |
| Why automation is no longer optional in 2026 | Business | Inspirational |
| Common mistakes in lead generation | Sales | Educational |
| How to close deals faster with AI tools | Sales | Professional |

## Requirements

- n8n instance (cloud or self-hosted)
- OpenAI API key
- Google Sheets OAuth2 credentials
- LinkedIn OAuth2 credentials
- Twitter/X API credentials (OAuth1)

## Tech Stack

- **n8n** — workflow automation
- **OpenAI GPT-4o-mini** — content generation
- **Google Sheets** — content queue management
- **LinkedIn API** — post publishing
- **Twitter/X API v2** — tweet publishing

---

Built by [Nurmuhammad Adkhamjonov](https://github.com/nurikk-66) — AI Automation Engineer
