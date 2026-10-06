# Cyber Pulse - move from GitHub Pages to Vercel

This gives the Pulse its AI features (news analysis + News Analyzer), which need serverless
functions that GitHub Pages cannot run. Your domain (CNAME) stays the same.

## Files
- index.html      - the Pulse page (feed + News Analyzer + per-article AI briefing + share)
- api/analyze.js  - reads an article URL and returns a structured briefing (NVIDIA)
- api/news.js     - live feed: RSS + NVD CVEs + CISA KEV (in-memory cache)

## Steps
1. In the cyber-pulse repo, UPLOAD these files:
   - index.html  (replaces the old one)
   - the api/ folder (api/analyze.js and api/news.js)
   You can keep news.json, scripts/ and the workflow - they're harmless, but no longer required.
   Keep the CNAME file so your domain is preserved.
2. Import the cyber-pulse repo into Vercel (vercel.com -> Add New -> Project -> cyber-pulse -> Deploy).
3. In the Vercel project: Settings -> Environment Variables, add:
   - NVIDIA_API_KEY = your nvapi-... key
   - NVIDIA_MODEL   = meta/llama-3.2-11b-vision-instruct   (optional but recommended)
   Then Deployments -> Redeploy.
4. Move the domain: in Vercel -> Settings -> Domains, add the domain that's in your CNAME.
   Vercel shows the DNS records to set at your registrar. Once it points to Vercel,
   turn OFF GitHub Pages for this repo (Settings -> Pages -> Source: None) to avoid a conflict.

## Verify
- Open your Pulse domain: the feed loads, clicking an item opens the AI briefing,
  and the "News Analyzer" tab analyses any pasted URL.
