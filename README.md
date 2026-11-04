# MINIMAL LABEL | SILVER LINE

Static GitHub Pages jewelry catalogue with a protected Supabase-backed administrator screen.

## Included

- `index.html`: customer catalogue, 6 starter products, categories, search, shopping list, Instagram/Messenger links.
- `admin.html`: admin-only sign in; create, edit, delete and publish/unpublish products; upload/remove multiple images; price, descriptions, categories, availability, display order; social links; JSON backup.
- `supabase-setup.sql`: Postgres tables, grants, row-level security and Storage policies.
- `config.js`: **public** Supabase project URL and publishable/anon key. Never paste secret / `service_role` keys into this file.
- `assets/`: 6 starter product photos.

## First-time setup (required for live editing)

1. Create a Supabase project: https://supabase.com/dashboard (project creation is performed in your Supabase account, not inside GitHub).
2. From **SQL Editor**, run `supabase-setup.sql`.
3. In **Authentication → Users**, create/invite your admin email and set a strong password. If using the invitation flow, ensure the account finishes email verification. You do not need to give passwords to anyone else.
4. Copy the new admin user's UUID from Authentication → Users. In SQL Editor run:
   ```sql
   insert into public.admin_users(user_id) values ('YOUR-REAL-USER-UUID');
   ```
   Never use an email address or password in that query, only the UUID.
5. From **Project Settings → API Keys**, obtain the **Project URL** and a **publishable key** (legacy `anon` key is also supported). Edit the two strings in `config.js` and commit. These two values are intended to be public; **do not publish secret or service_role keys**.
6. Make sure your GitHub repository's Pages setting uses `main` / `/ (root)`.
7. Visit `https://mari-4m.github.io/minimal-label/admin.html`, sign in with the approved admin account, and press **საწყისი 6 პროდუქტის დამატება** once. The starter items will become live shared catalog records. They initially show prices 59, 42, 51, 68, 47 and 40 GEL respectively, and can be edited anytime.
8. Enter Instagram and Facebook usernames in the admin settings and Save.

## Data behaviour

Before Supabase is configured, the public site displays the 6 bundled starter items and prices, but there is no shared editing. When connected, the public site loads the `products` and `site_settings` tables and checks for updates when the page is reopened, revisited, and periodically while it is open. The catalog displays only published items. Users cannot create or change products because server-side Postgres RLS and Storage policies limit writes to members of `admin_users`.

This is a catalogue, **not** a payment processor. Orders are made by copying the shopping list and contacting the shop on Instagram or Messenger. GitHub Pages does not by itself provide authentication, shared data storage or order/payment handling.

## Notes on 925 badges

The starter photos include an existing 925 badge for illustrative purposes. Confirm the silver composition with the supplier before advertising an item as 925 sterling silver. Gold-tone items might be gold-plated silver or a different material; the photo alone does not prove the alloy.

## Security checklist

- Enable MFA for your Supabase and GitHub accounts.
- Keep Supabase policies active and never expose secret/service-role API keys.
- Disable open public signup if only the administrator will use the site.
- Before accepting real customer data, review data retention and privacy policy. This first version does not store customer details.
- Review images and descriptions for accurate product claims.
