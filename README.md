# The Open Championship Golf Pool at Royal Birkdale

Complete Netlify app for a 4-player-group golf pool for **The Open Championship** at **Royal Birkdale**.

## Version

v3

## What this app does

- Accepts entrant groups by CSV upload or manual entry.
- Each group has exactly 4 golfers.
- Preserves the uploaded group label exactly, such as `Group 1` or `Group 2`.
- Calculates group scores from the configured live golf feed.
- Supports RapidAPI Golf Leaderboard Data by setting Netlify environment variables.
- Uses `holes_played` for the Thru value when supplied by Golf Leaderboard Data.
- Treats cut golfers as `Missed Cut`, including `cut`, `mc`, `missed cut`, `did not make cut`, and `dnmc`.
- Missed Cut golfers count toward Risk and receive the Missed Cut Penalty.
- Withdrawn golfers count toward Risk and receive the Withdrawn Penalty.
- Admin functions remain disabled until an Admin PIN is entered.

## CSV format

Use this header:

```csv
entrant,groupLabel,golfer1,golfer2,golfer3,golfer4
```

The `groupLabel` value is shown exactly on the leaderboard.

Template included:

```text
open_championship_pool_entrants_template.csv
```

## Netlify deployment

Upload these files at the GitHub repo root:

```text
package.json
netlify.toml
public/
netlify/functions/
README.md
.env.example
open_championship_pool_entrants_template.csv
```

Do not upload a parent wrapper folder. `package.json` must be at the GitHub repo root.

Netlify build settings:

```text
Build command: npm run build
Publish directory: public
Functions directory: netlify/functions
```

## Netlify environment variables

Start with demo mode:

```text
ADMIN_PIN=your-private-pin
LIVE_GOLF_PROVIDER=demo
CACHE_SECONDS=60
REFRESH_SECONDS=60
```

For RapidAPI Golf Leaderboard Data, after you find The Open Championship / Royal Birkdale fixture ID:

```text
LIVE_GOLF_PROVIDER=rapidapi
RAPIDAPI_KEY=your_rapidapi_key
RAPIDAPI_HOST=golf-leaderboard-data.p.rapidapi.com
RAPIDAPI_URL=https://golf-leaderboard-data.p.rapidapi.com/<live-leaderboard-endpoint>?id=<OPEN_CHAMPIONSHIP_FIXTURE_ID>
CACHE_SECONDS=60
REFRESH_SECONDS=60
```

If Netlify Blobs requires manual credentials:

```text
NETLIFY_BLOBS_SITE_ID=your-netlify-site-id
NETLIFY_BLOBS_TOKEN=your-netlify-personal-access-token
```

## Deploy

After replacing the repo contents:

```text
Deploys → Trigger deploy → Clear cache and deploy site
```

Then open:

```text
https://your-site-name.netlify.app/?v=3
```

## Test endpoints

```text
/api/pool
/api/live-leaderboard
/app.js?v=3
```


## v3 branding update

- Restores the same footer branding used in the prior KOS/TRG app:
  - KOS logo
  - Kings of Swing Golf Group
  - Powered by TRG
- Keeps The Open Championship / Royal Birkdale event identity in the header and footer detail line.


## v3 deploy fix

- Replaced `netlify.toml` with a clean valid TOML file.
- Keeps KOS logo, Kings of Swing Golf Group, and Powered by TRG footer branding.
- Use `?v=3` after deploy.
