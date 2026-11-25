# MLBB Nexus — upgraded project

React + Vite dashboard using the original warm cream / black / red visual theme.

## What's included
- Supabase email/password sign-up, sign-in, persistent session, sign-out and password-reset email.
- Demo dashboard access removed.
- Live hero rank request integration against the community-maintained Rone Arena API.
- Rank and sort filters; live data error/empty/loading states.
- Counter lookup and academy build endpoint requests.
- Player ID + Zone ID lookup form with an explicit limitation message (the documented player data endpoints require in-game email verification and provider-issued auth; there is no guaranteed public ID-only profile endpoint).
- India INR store catalogue and order enquiry UI. Prices are placeholders, no payment is collected, and no order is transmitted/fulfilled.
- Mobile responsive navigation and Vercel SPA rewrite.
- `supabase-schema.sql` starter profile table with row-level security.

## Local setup
1. Install Node.js 20+.
2. Run `npm install`.
3. Copy `.env.example` to `.env`.
4. Fill in Supabase project URL and anon/public key.
5. Run `npm run dev`.

## Supabase authentication setup
1. Create a Supabase project.
2. Enable Authentication → Providers → Email.
3. For testing, configure email confirmation under Authentication settings. If confirmation is enabled, users must confirm their email before login.
4. Copy Project URL and anon/public key from Project Settings → API into `.env`.
5. Add local and deployed URLs under Authentication → URL Configuration.
6. Run `supabase-schema.sql` in SQL Editor if you want the starter profiles table.
7. Never expose the Supabase service-role key in a Vite `VITE_` variable.

## Vercel deploy
- Import the GitHub repository into Vercel.
- Framework: Vite
- Build: `npm run build`
- Output: `dist`
- Add `VITE_SUPABASE_URL`, `VITE_SUPABASE_ANON_KEY`, and optionally `VITE_MLBB_API_BASE` in Project Settings → Environment Variables.
- Redeploy after changing environment variables.
- Add the deployed Vercel domain to Supabase Auth URL Configuration.

## Live data and limitations
The hero rankings/counter/build integrations use the public, community-maintained Rone Arena API (`https://arena.fastapicloud.dev/api`). It is unofficial, subject to provider availability, rate limits, CORS behavior and response changes. It is not Moonton-operated or guaranteed. The website shows a clear error state if the provider is unavailable. Verify current API terms and usage limits before public launch.

Player lookup is not presented as working ID-only profile retrieval: the provider documents authenticated player endpoints and an in-game email verification flow. Do not ask players for their MLBB password or verification code. To add secure account linking, implement the provider's official documented flow and handle tokens server-side where possible.

Player leaderboards are not fabricated. A verified player ranking feed must be connected before this feature can show actual top global/India players.

## Store / payments
The catalogue prices are editable placeholders, not verified official Indian retail prices. The current order form is a UI preview only. Before selling, obtain authorized reseller/supplier access, confirm applicable platform and regional rules, choose a payment gateway, and implement server-side order creation, signed payment webhook verification, idempotency, refunds and fulfilment tracking. Never fulfil based only on a browser success redirect.

## Test before publishing
- `npm run build`
- Test sign-up, email confirmation, sign-in, password reset, refresh persistence and logout.
- Test hero API availability and error handling.
- Verify store prices and supplier authorization before accepting money.
- Test mobile and desktop widths.

Unofficial fan project. Not affiliated with or endorsed by Moonton. All Mobile Legends: Bang Bang names and marks belong to their respective owners.
