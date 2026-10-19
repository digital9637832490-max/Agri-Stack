# Farmer Profile Portal — separate project starter

This is a **new, separate project**. The previous card studio has been copied unchanged into `legacy-card-studio/` for reference/backup; it is also served at `/legacy-card-studio/` when the Node server is running.

## Included
- User registration and phone OTP sign-in (5-minute expiry, hashed OTP, attempt limit)
- Admin ID + password sign-in (no OTP)
- Admin dashboard with user counts, profile IDs, paid revenue, payment history, and user access enable/disable
- ₹30 Razorpay order creation and server-side signature + captured-payment verification before a paid user profile is created
- Admin can create profile IDs for free
- Separate SQLite database

## Important limitations
- These are **portal-specific personal profile IDs**, not government-issued or verified Farmer Registry / AgriStack IDs. No government registry integration is included.
- Live SMS and payments will **not work until you configure provider credentials**. Twilio SMS is supported as a basic integration; credentials and an approved sending number are required. Razorpay test keys should be used before live mode.
- This is a starter implementation, not a security-audited production service. Before public launch, add HTTPS/reverse proxy, persistent database/backups, privacy notice and consent, stronger operational monitoring, payment reconciliation/refund handling, account recovery, and a security review. Hosting only on GitHub Pages cannot run this backend.

## Run locally
Requires Node.js 20+.

1. Copy `.env.example` to `.env`.
2. Set `JWT_SECRET` to a random string of at least 32 characters.
3. Generate an admin password hash:
   ```bash
   node -e "console.log(require('bcryptjs').hashSync('YOUR-STRONG-ADMIN-PASSWORD', 12))"
   ```
   Put the result in `ADMIN_PASSWORD_HASH`, and set `ADMIN_ID`.
4. For real SMS, fill in `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, and `TWILIO_FROM_NUMBER`. Without them, OTP is only printed to the server console in development mode. Never use that development mode in production.
5. Add Razorpay test credentials to `RAZORPAY_KEY_ID` and `RAZORPAY_KEY_SECRET`.
6. Install and run:
   ```bash
   npm install
   npm start
   ```
7. Open `http://localhost:3000`.

Do not commit `.env`, database files, credentials, or real farmer personal data to GitHub. Use HTTPS in deployment.
