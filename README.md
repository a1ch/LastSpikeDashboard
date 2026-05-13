# LSB Maintainer Dashboard

Azure Static Web App — maintenance dashboard for Last Spike Brewery.

## What it shows
- **Summary cards** — Overdue, Due This Month, Upcoming 90 days, WOs logged this month
- **Tabbed views** — Overdue / Due This Month / Upcoming 90d / All Tasks
- **Filters** — by Area, Responsible person, Frequency + free text search
- **Sort** — click any column header
- **Detail modal** — click any row for full task details

## Auth
Signs in with the user's `@lastspikebrewery.com` Microsoft account via OAuth implicit flow.
Reads live data from SharePoint via Graph API (`Sites.Read.All` scope).

## Deploy to Azure Static Web Apps

```bash
# Create the Static Web App (free tier)
az staticwebapp create \
  --name lsb-maintainer-dashboard \
  --resource-group <rg> \
  --source https://github.com/a1ch/LastSpikeDashboard \
  --location canadacentral \
  --branch main \
  --app-location "/" \
  --output-location "/"
```

## Required: Add redirect URI to App Registration
After deploying, add the Static Web App URL as a redirect URI in the Azure AD app registration:
1. Azure Portal → App registrations → LSB Maintainer app
2. Authentication → Add a platform → Single-page application
3. Redirect URI: `https://<your-static-web-app-url>/`
4. Enable: Access tokens, ID tokens

## Embed in SharePoint
1. Edit the Maintainer subsite home page
2. Add web part → Embed
3. Paste the Static Web App URL
