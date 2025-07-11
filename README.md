# Netlify Deploy Workflow

A reusable GitHub Actions workflow for deploying static websites to Netlify.

## Quick Setup

### 1. Create Workflow File

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Website via Reusable Netlify Workflow

on:
  workflow_dispatch:
  push:
    branches: [master]  # The name of the branch that triggered the push

jobs:
  call-deploy:
    uses: poyin-chen-appier/netlify-deploy-action/.github/workflows/deploy.yml@main
    with:
      build-dir: .  # The build directory
      site-id: ${{ vars.NETLIFY_SITE_ID }}
    secrets:
      NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
```

### 2. Set Up GitHub Variables

1. Go to your repository → **Settings** → **Secrets and variables** → **Actions**
2. Click **Variables** tab
3. Add repository variable:
   - **Name**: `NETLIFY_SITE_ID`
   - **Value**: Your Netlify site ID

### 3. Set Up GitHub Secrets

1. In the same page, click **Secrets** tab
2. Add repository secret:
   - **Name**: `NETLIFY_AUTH_TOKEN`
   - **Value**: Your Netlify auth token

### 4. Get Netlify Credentials

**Site ID**: Found in Netlify dashboard → Site Settings → General → Site information

**Auth Token**: 
1. Go to [app.netlify.com/user/settings/tokens](https://app.netlify.com/user/settings/tokens)
2. Click "New token"
3. Copy the generated token

## Usage

- **Auto-deploy**: Push to `master` branch, you can replace the branch name
- **Manual deploy**: Go to Actions tab → Select workflow → Run workflow

## Configuration

- **`build-dir`**: Directory with static files to deploy (default: `.`)
- **`site-id`**: Your Netlify site ID
- **`NETLIFY_AUTH_TOKEN`**: Your Netlify auth token

## Requirements

- Your project must contain static files (HTML, CSS, JS, images, etc.)
- No build process required - files are deployed as-is