# ⚡ Facebook AI Agent — GHL Expert Edition

A complete AI-powered Facebook marketing agent that generates content using Russell Brunson's frameworks, publishes to your page, monitors groups for leads, and more.

---

## Quick Start (3 minutes)

### 1. Install dependencies

```bash
npm install
```

### 2. Create your .env file

```bash
cp .env.example .env
```

Then open `.env` and fill in your keys:

```
FB_ACCESS_TOKEN=EAAxxxxxxx...       # From Graph API Explorer
FB_PAGE_ID=123456789012345           # Your Facebook Page ID
ANTHROPIC_API_KEY=sk-ant-xxxxxxx... # From console.anthropic.com
PORT=3001
```

### 3. Run the agent

```bash
npm run dev
```

This starts both:
- **Backend server** on `http://localhost:3001` (handles API keys securely)
- **Frontend dashboard** on `http://localhost:5173` (your control panel)

Open `http://localhost:5173` in your browser.

---

## How It Works

### Architecture

```
Browser (React)  →  Express Backend  →  Anthropic API (content generation)
                                     →  Facebook Graph API (publishing)
```

Your API keys **never touch the browser**. Everything goes through the Express server.

### Features

| Feature | Status | Description |
|---------|--------|-------------|
| Content Generation | ✅ Live | 5 Russell Brunson frameworks with GHL-specific prompts |
| Post Scheduling | ✅ Live | Queue posts, auto-publish at 9 AM & 9 PM daily |
| Publish to Facebook | ✅ Live | One-click publish through Graph API |
| Group Monitoring | 🔶 Demo | Scans for hiring/GHL posts (mock data, real reply generation) |
| Reply Generation | ✅ Live | AI-crafted personalized replies to group posts |
| Lead Scraping | 🔶 Demo | Dream customer avatar matching (mock data) |
| Friend Requests | 🔶 Demo | Queue system ready (needs browser automation) |

### Russell Brunson Frameworks

1. **Hook → Story → Offer** — Pattern interrupt + relatable story + CTA
2. **Epiphany Bridge** — Share your "aha moment" to create belief
3. **Attractive Character** — Build persona through backstory & flaws
4. **Soap Opera Sequence** — Open loops & cliffhangers
5. **Pure Value Bomb** — Give away your best stuff for authority

---

## Getting Your Facebook Credentials

### Access Token

1. Go to [developers.facebook.com/apps](https://developers.facebook.com/apps)
2. Create a new app (type: Business)
3. Open [Graph API Explorer](https://developers.facebook.com/tools/explorer)
4. Select your app from the dropdown
5. Click "Get Token" → "Get User Access Token"
6. Check permissions: `pages_manage_posts`, `pages_read_engagement`, `pages_read_user_content`
7. Copy the token into your `.env` file

**For a long-lived token (60 days):**
```
https://graph.facebook.com/v19.0/oauth/access_token?grant_type=fb_exchange_token&client_id=YOUR_APP_ID&client_secret=YOUR_APP_SECRET&fb_exchange_token=YOUR_SHORT_TOKEN
```

### Page ID

- Go to your Facebook Page → About → Page Transparency → Page ID
- Or in Graph API Explorer, query `/me/accounts` to see all your pages with IDs

---

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/health` | GET | Server status + config check |
| `/api/generate` | POST | Generate content via Claude |
| `/api/publish` | POST | Publish post to Facebook |
| `/api/comments/:postId` | GET | Fetch comments on a post |
| `/api/comments/:commentId/reply` | POST | Reply to a comment |
| `/api/queue` | GET/POST | Manage post queue |
| `/api/queue/:id` | DELETE | Remove from queue |
| `/api/scheduler/toggle` | POST | Enable/disable auto-posting |

---

## Troubleshooting

| Error | Fix |
|-------|-----|
| "Backend server not running" | Run `npm run dev` in your terminal |
| "ANTHROPIC_API_KEY not set" | Add your key to the `.env` file |
| Facebook "OAuthException" | Your token expired — generate a new one |
| "Network error" | Check your internet connection |
| Port already in use | Change `PORT` in `.env` or kill the process on that port |

---

## Production Notes

- **Never commit your `.env` file.** It's in `.gitignore`.
- For real group monitoring, you'd need Facebook Group API access (requires admin approval).
- Friend request automation may violate Facebook ToS — use the queue system with human review.
- Consider adding a database (SQLite/PostgreSQL) to persist queue and history across restarts.
