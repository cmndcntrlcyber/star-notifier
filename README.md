# GitHub Stars to Discord Notifier

Automatically sends a Discord message whenever you star a new GitHub repository.

## Setup Instructions

### 1. Create a new GitHub repository

Create a new **private** repository (e.g., `star-notifier`) and add the workflow file.

### 2. Create a Discord Webhook

1. Open your Discord server
2. Go to **Server Settings** → **Integrations** → **Webhooks**
3. Click **New Webhook**
4. Choose the channel where notifications should appear
5. Copy the webhook URL

### 3. Add Repository Secrets and Variables

In your new repository, go to **Settings** → **Secrets and variables** → **Actions**

**Add a Secret:**
- Name: `DISCORD_WEBHOOK_URL`
- Value: Your Discord webhook URL from step 2

**Add a Variable:**
- Go to the **Variables** tab
- Name: `GH_USERNAME`
- Value: Your GitHub username

### 4. Initialize the data file

Create a `data/known_stars.txt` file in your repository. You can leave the file empty to get notifications for all future stars, or pre-populate the file with your existing starred repos (one per line in `owner/repo` format) to only get notifications for new stars.

To get your current stars and avoid duplicate notifications:

```bash
gh api "/users/YOUR_USERNAME/starred?per_page=100" --jq '.[].full_name' > data/known_stars.txt
```

### 5. Enable GitHub Actions

1. Go to the **Actions** tab in your repository
2. Enable workflows if prompted
3. You can manually trigger the workflow using "Run workflow" to test

## How the Notifications Look

Each notification includes:
- ⭐ Repository name (clickable link)
- Description
- Programming language
- Current star count
- Repository owner's avatar

## Customization

- **Frequency**: Edit the cron schedule in the workflow file (default: every 15 minutes)
- **Embed appearance**: Modify the Discord embed JSON in the workflow to change colors, fields, etc.

## File Structure

```
your-repo/
├── .github/
│   └── workflows/
│       └── star-notifier.yml
├── data/
│   └── known_stars.txt
└── README.md
```
