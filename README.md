# Stockholm Transit – Live Digital Shadow

A live dashboard for the Stockholm metro (Tunnelbana) and commuter rail (Pendeltåg), built for teaching artificial intelligence and digital twin concepts.

## Features

- Map of the metro (lines 10, 11, 13, 14, 17, 18, 19) and commuter rail (lines 40, 41, 43, 44); each network can be shown or hidden
- Estimated live train positions; trains delayed by 2 minutes or more are outlined in red
- Search any station or stop on the SL network, including bus, tram and boat stops
- Indicators for the selected stop: next departure, departures in the next 30 minutes, average delay, on-time rate, trains due in the next 10 minutes, cancellations, a departure board, departures per 10-minute window and service alerts
- Switch between schematic and geographic views
- Falls back to simulated data automatically when the live feed is unavailable

Data source: [SL Transport API](https://www.trafiklab.se/api/other-apis/sl/transport/) (no API key required). See the SL/Trafiklab licence terms for data usage.

## How it works

The site is fully static, with no server code. `netlify.toml` forwards requests made to `/v1/...` through Netlify to the SL API, so the browser talks to the same domain and no CORS issues occur.

## Deploying from GitHub to Netlify

1. Push these files to a GitHub repository (`index.html`, `netlify.toml`, `README.md`).
2. Sign in at [app.netlify.com](https://app.netlify.com) with your GitHub account.
3. Choose **Add new site > Import an existing project > GitHub** and select the repository.
4. Leave the build settings empty; they are read from `netlify.toml`.
5. Click **Deploy**. The site goes live at `https://SITE-NAME.netlify.app`.

Every change pushed to GitHub is redeployed on Netlify automatically. You can rename the site under **Site configuration > Change site name**.

## Limitations

- Train positions are not GPS-based; they are estimated from each station's next-departure predictions.
- Commuter rail stop patterns are simplified. If SL changes them, edit the `LINES` section in `index.html`.
- Station names that cannot be matched to SL records are listed in the status message at the top of the side panel.
- The system only observes trains and cannot control them, so it is a **digital shadow** rather than a true digital twin.
