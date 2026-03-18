# X.com Inspiration Fetcher (Prototype)

This repo contains a small prototype that fetches *recent X.com posts* based on a set of **keywords** and **accounts** you want to monitor.

## ✅ What it does
- Runs **search queries** using X API `GET /2/tweets/search/recent`
- Uses the supplied **keyword clusters** and **accounts** to build queries
- Stores the raw JSON responses in `data/x/` for later processing or draft generation

## 🚀 Quick start

### 1) Create an X Developer app & get a bearer token
1. Go to https://developer.x.com/
2. Sign in and create a Project + App
3. Under **Keys and tokens**, copy the **Bearer token**

### 2) Configure your environment
```bash
cp .env.example .env
# edit .env and paste your bearer token into X_BEARER_TOKEN
```

### 3) Install dependencies (Node 18+ required)
```bash
npm install
```

### 4) Run the fetch script (via X API)
If your X Developer account has credits, run:
```bash
npm run fetch:x
```

### 5) (Alternative) Run the scraper (no X API credits needed)
If you don’t have credits, run the scraper instead. It uses **Nitter** (an open X/Twitter frontend) to fetch public posts.

```bash
npm run scrape:x
```

If you need to use a different Nitter instance (e.g., if the default is rate-limited), set:

```bash
export NITTER_INSTANCE=https://nitter.net
# or another public instance like https://nitter.1d4.us
npm run scrape:x
```

### 6) Generate post drafts (Claude)
After scraping, generate draft posts from the results using **Claude**.

1) Ensure your key is set (preferred):
```bash
export CLAUDE_API_KEY="claude-..."
export CLAUDE_MODEL="claude-opus-4-6"
```

If you still want to use OpenAI instead, you can set:
```bash
export OPENAI_API_KEY="sk-..."
```

2) Run draft generation:
```bash
npm run drafts:generate
```

Drafts are written to `data/drafts/`.

### 7) Review results
- X API output: `data/x/` (one JSON file per query)
- Scraper output: `data/x-scrape/` (one JSON file per query)
- Generated drafts: `data/drafts/` (one JSON file per source)

## 🔧 Customization
- Update keyword clusters and accounts in `src/config.js`.
- Tweak query behavior (language, retweet filtering, max results) in `src/fetchX.js`.

## Next steps (suggested)
- Use the fetched data to generate post drafts via Claude.
- Build a small UI (Next.js) to approve/edit drafts.
- Integrate Webflow publishing.
