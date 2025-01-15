# GitHub Integration with {{ product.sandbox }}

## Overview

{{ product.sandbox }} enables a top-down approach to business automation by allowing you to:

- Create decision and process models
- Publish projects directly to various Git providers
- Synchronize changes between {{ product.sandbox }} and Git
- Deploy projects through traditional deployment pipelines

## Connecting to GitHub

### Generate a GitHub Token

1. Go to your GitHub account settings
2. Navigate to **Developer settings** → **Personal access tokens** → **Tokens (classic)**
3. Click **Generate new token**
4. Configure your token:

   ```{ .yaml .copy }
   Name: {{ product.sandbox }} Integration  # Or any meaningful name
   Expiration: Choose between 30, 60, 90 days or no expiration
   Required scopes:
     - repo (Required)
     - gist (Required)
   Optional scopes:
     - workflow
     - write:packages
     - read:packages
   ```

!!!tip

    Copy your token immediately after generation - it won't be shown again
    Keep your token secure - it provides access to your GitHub account

### Connect {{ product.sandbox }} to GitHub

1. In {{ product.sandbox }}, click the User icon in the top navigation
2. Select **Connect to an account**
3. Choose **GitHub** from the provider options
4. Click **Generate new token** if you haven't already generated one
5. Paste your GitHub token in the connection wizard
6. Verify the connection is successful - you should see:
   - Your GitHub username
   - Connection status
   - Available repositories

## Next Steps

After connecting GitHub to {{ product.sandbox }}, you can:

- Create new projects
- Sync existing projects
- Manage version control directly from the {{ product.sandbox }} interface
- Deploy your projects using standard CI/CD pipelines

!!! tip

    Keep your token's expiration date in mind - set a reminder to regenerate it before it expires to maintain continuous integration.
