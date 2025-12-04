# Azure Static Web Apps

Azure Static Web Apps is designed for client-side applications (such as SPAs) and is not suitable for server-side hosting.

## Setup

To create a new Static Web App:

### Basics

1. Go to the Azure Portal and start creating a Static Web App.
2. Under the **Basics** tab, select the appropriate resource group and provide a name (e.g., `stapp-terstal-webapp-frontend-prod`).
3. Choose the hosting plan:
    - **Standard** for production applications (provides uptime guarantees).
    - **Free** for non-production use.
4. Set the deployment source to **Other**. (You will configure GitHub Actions manually.)

### Deployment Configuration

Select **Deployment Token** as the deployment method.

### Advanced

Leave the default values unless you have specific requirements.

### Tags

Add tags only if necessary for resource management.

## Deployment

To deploy code to your Static Web App:

1. In the Azure Portal, go to the Overview page of your Static Web App.
2. Click **Manage Deployment Token** and save the token.
3. In your GitHub repository, add this token as a secret under **Settings > Actions > Secrets**. Name the key appropriately (e.g., `AZURE_STATIC_WEB_APPS_API_TOKEN`).
4. Add the following GitHub Action workflow to `.github/workflows/main.yaml`:

```yaml
name: Deploy web app to Azure Static Web Apps

permissions:
    id-token: write
    contents: read
    pull-requests: write

on:
    push:
        branches:
            - main
            - development

jobs:
    build-and-deploy:
        runs-on: ubuntu-latest
        name: Build and Deploy
        steps:
            - name: "Checkout"
              uses: actions/checkout@v5

            - name: Set Deployment Variables
              id: set-vars
              run: |
                  echo "Detected branch: $GITHUB_REF"
                  if [ "$GITHUB_REF" = "refs/heads/main" ]; then
                      echo "VITE_BACKEND_URL=https://api.terstal.remcoloof.nl" >> $GITHUB_ENV
                      echo "AZURE_STATIC_WEB_APPS_API_TOKEN=${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_PROD }}" >> $GITHUB_ENV
                  elif [ "$GITHUB_REF" = "refs/heads/development" ]; then
                      echo "VITE_BACKEND_URL=https://api.terstal.dev.remcoloof.nl" >> $GITHUB_ENV
                      echo "AZURE_STATIC_WEB_APPS_API_TOKEN=${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN_DEV }}" >> $GITHUB_ENV
                  fi
            - name: Build And Deploy
              uses: Azure/static-web-apps-deploy@1a947af9992250f3bc2e68ad0754c0b0c11566c9
              with:
                  azure_static_web_apps_api_token: ${{ env.AZURE_STATIC_WEB_APPS_API_TOKEN }}
                  action: "upload"
                  app_location: "/"
                  output_location: "dist"
              env:
                  # add environment variables, which are listed in your .env here
```

## Custom Domains

To add a custom domain:

1. In the Azure Portal, go to **Custom Domains** for your Static Web App.
2. Click **Add > Custom domain on other DNS** and enter your domain name.
3. Add the required CNAME and TXT records to your DNS provider.
4. Validate and add the domain in Azure. (DNS changes may take up to 48 hours to propagate.)

## Troubleshooting

### SPA 404 on Page Refresh

If refreshing a page in your Single Page Application (SPA) results in a 404 error, this is typically due to missing navigation fallback configuration. To resolve this:

1.  Create a file named `staticwebapp.config.json` in your app's static folder.
2.  Add the following content:

        ```json
        {
            "navigationFallback": {
                "rewrite": "/index.html"
            }
        }
        ```

This configuration ensures that all navigation requests fallback to `index.html`, allowing client-side routing to work correctly.
