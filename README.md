# Lumbercorp Faction Intel

A responsive Torn faction dashboard showing lifetime drug use, daily and weekly overdose changes, and weekly boosters and consumables.

## Deploy to Render

1. Extract this package and place `index.html`, `render.yaml`, and `.gitignore` at the root of a Git repository.
2. Push that repository to your Git provider.
3. In Render, select **New → Blueprint**, connect the repository, and deploy. Render reads `render.yaml` and creates a Static Site.
4. Open the generated HTTPS site URL. Select **Connect API** and enter your Torn public-access key in the app.

Do not add your Torn API key to the repository or Render environment variables. Each user supplies their own key in the browser.

### Alternative: manual Static Site setup

Select **New → Static Site**, connect the repository, and use:

- **Name:** `lumbercorp-faction-intel`
- **Build command:** `mkdir -p public && cp index.html public/index.html`
- **Publish directory:** `public`
- **Root directory:** leave blank when these files are at the repository root
- **Environment variables:** none

If you place the app in a subdirectory, set the manual site's Root Directory to that folder. The included Blueprint assumes the app files are at the repository root.

## Data and privacy

- API requests go directly from the browser to `https://api.torn.com/v2/`.
- Keys stay only in the current tab's JavaScript memory; they are not stored in local storage, sent to Render, or embedded in files. Reloading clears them.
- The app starts with clearly labelled demo data.
- Public access is sufficient for the requested Torn endpoints.
- Lifetime totals include activity before joining the faction.
- Daily and weekly counts subtract historical stats requested approximately one and seven days earlier. Torn rounds historical requests to dates, so these are not precise rolling windows.
- Missing values show a dash and are excluded from the relevant totals.
- Booster categories are displayed separately, not summed into a potentially misleading combined total.
- Requests are paced at about 48 per minute. A full sync uses up to five requests per member plus two faction requests. A 100-member faction can take roughly 11 minutes or more. Other apps using the same key or IP can affect rate limits.
- No background scheduler or persistent history is included. Use Refresh data to sync again.

## Local preview

With Python 3 installed:

```sh
python -m http.server 3000 --bind 0.0.0.0
```

Open `http://localhost:3000` in your browser.

## Deployment checks

1. Confirm the page opens over HTTPS with the Lumbercorp branding.
2. Check demo cards, member search, sorting, and CSV export.
3. Connect a valid public Torn key and wait for the full sync.
4. Verify your faction roster, lifetime stats, and historical coverage.
5. Reload and confirm that the key has been cleared.

The static build and JavaScript syntax were checked locally. A real Render deployment and authenticated Torn API sync still need validation with your account. This is an independent fan tool, not affiliated with Torn.
