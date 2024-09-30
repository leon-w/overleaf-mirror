# overleaf-mirror

This repository template allows you to automatically sync an Overleaf project with a GitHub repository using GitHub Actions.
The contents of the Overleaf project will be copied to the `latex/` directory in this repository.

## Getting Started

### Step 1: Create a Repository from this Template

Click on Use this template at the top of this repository.
Create your new repository.

### Step 2: Configure Secrets

In your newly created repository, go to _Settings > Secrets and variables > Actions > New repository secret_.

Add the following secrets:

| Secret Name            | How to Get                                                                                                                |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `LATEX_SESSION_COOKIE` | Log in to Overleaf, open the browser developer tools, inspect a request, and locate the cookie named `overleaf_session2`. |
| `LATEX_PROJECT_ID`     | Go to your Overleaf project and note the project ID in the URL. Example: `https://www.overleaf.com/project/<PROJECT_ID>`  |

### Step 3: Configure the Sync Schedule

To automatically sync on a schedule, update the cron job in the `.github/workflows/sync.yml` file and configure the schedule using the [cron syntax](https://crontab.guru/):

```yaml
on:
  schedule:
    - cron: "0 * * * *"
```

**Important:**
Each invocation of the workflow will use at least 1 minute of your GitHub Actions minutes quota.
The default quota is 2000 minutes per month, so you can run the workflow up to 2000 times per month for free.
To stay within the free tier, avoid running the workflow more often than every 30 minutes and turn off the workflow when you don't need it.
