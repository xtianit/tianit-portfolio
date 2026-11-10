# tianit.online

Portfolio site (static `index.html`) plus a small payment API (`api/`) that runs on Vercel.

## Deploy from scratch
1. **Rotate keys first** (they were shared in a chat): Paystack > Settings > API Keys > generate a new secret key; Brevo > delete the old key and create a new **API** key.
2. **Delete the old setup**: Vercel project > Settings > Delete (this frees `www.tianit.online`), then the old GitHub repo > Settings > Delete.
3. **New GitHub repo**, empty, no README. In this folder (Windows terminal):
   ```
   git init
   git add .
   git status        (make sure .env is NOT listed)
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/xtianit/YOUR-NEW-REPO.git
   git push -u origin main
   ```
4. **Vercel** > Add New > Project > import the repo. Framework Preset: **Other**. Leave Build and Output settings empty.
   Before deploying, add Environment Variables (all in `.env.example`). Deploy.
5. **Domain**: Project > Settings > Domains > add `www.tianit.online` (and `tianit.online`, set to redirect to www).
6. Open `https://www.tianit.online/health`. It should show `ok`.
7. **Paystack** > Settings > API Keys & Webhooks > Test Webhook URL: `https://www.tianit.online/api/paystack-webhook`.
8. Make a test payment (Paystack test card), then check Vercel > Logs for any error.

## Run locally
```
npm install
copy .env.example .env      (then fill in .env; set SITE_URL=http://127.0.0.1:5500)
npm start                   (API on http://localhost:3000)
```
Open `index.html` with Live Server (port 5500). The page automatically uses the local API when opened locally.

## Changing prices
Update the pricing cards and `PLANS` in `index.html`, the JSON-LD block, and `PLANS` in `api/_server.js` together.
