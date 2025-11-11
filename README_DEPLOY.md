# Render Deploy Kit (Shippo + Razorpay Wallet Panel)

This kit adds the files needed for one‑click deploy on **Render**.

## Files
- `render.yaml` (root) – blueprint that creates two services on Render:
  - `shippo-backend` (Express)
  - `shippo-frontend` (React static site)
- `backend/.env.example` – copy/paste these keys in Render backend service
- `frontend/.env.example` – local dev config (not used by Render if you keep the rewrite)

## How to use
1. Upload these files into your GitHub repo root (same level as `/backend` and `/frontend`).
2. Commit to `main`.
3. Click: https://render.com/deploy?repo=<YOUR_REPO_URL>
4. After deploy, set backend environment variables in Render:
   - SHIPPO_API_TOKEN (from Shippo)
   - MARKUP_PERCENT=5
   - RAZORPAY_KEY_ID / RAZORPAY_KEY_SECRET / RAZORPAY_WEBHOOK_SECRET
   - FX_CACHE_TTL=600
5. When both services are live, edit `render.yaml` to replace the frontend route destination with your real backend URL:
   `destination: https://shippo-backend-xxxxx.onrender.com/*`
   Commit & push again to redeploy the frontend.

## Optional
- Add Razorpay webhook:
  - URL: `https://<backend-host>/api/razorpay/webhook`
  - Secret: your `RAZORPAY_WEBHOOK_SECRET`
  - Event: `payment.captured`
