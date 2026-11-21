# AURUM

Luxury perfume store for Bangladesh. Shop, cart, checkout, accounts, order tracking, studio desk, and rider desk.

## Run

```bash
npm install
npm run dev
```

Open the site on port 8080.

## What is saved

- Products, orders, profiles, wishlist, and payment attempts live in Postgres.
- With no `DATABASE_URL`, the app uses embedded Postgres in the preview.
- On deploy, set `DATABASE_URL` to Neon or any Postgres. Migrations in `migrations/` apply on build.

## Accounts

Email and password, plus Google and X. The first signed-in person can claim the studio desk once. From the studio desk, set another account’s role to `courier` for the rider desk.

## Payments

Cash on delivery places a real order and stays unpaid until delivery.

bKash and Nagad are wired to official merchant calls. They do **not** mark an order paid unless the gateway confirms it. Until you add keys, those orders stay `Awaiting Payment`.

Set these on the server (never in the browser):

| Provider | Variables |
| --- | --- |
| bKash | `BKASH_APP_KEY`, `BKASH_APP_SECRET`, `BKASH_USERNAME`, `BKASH_PASSWORD`, optional `BKASH_BASE_URL`, `BKASH_CALLBACK_URL` |
| Nagad | `NAGAD_MERCHANT_ID`, `NAGAD_MERCHANT_NUMBER`, `NAGAD_MERCHANT_PRIVATE_KEY`, `NAGAD_PG_PUBLIC_KEY`, `NAGAD_BASE_URL` |

bKash sandbox base URL used when `BKASH_BASE_URL` is empty: `https://tokenized.sandbox.bka.sh/v1.2.0-beta`.

## Coupons

`AURUM10` (10%), `WELCOME15` (15%), `LUXURY20` (20%). Delivery is ৳80 inside Dhaka, Gazipur, and Narayanganj, otherwise ৳150.

## Pages

- `/` home
- `/shop` collection, search, categories
- `/product/:slug` bottle
- `/cart` bag
- `/checkout` order
- `/track` order id + phone
- `/account` wishlist and history
- `/login` sign in
- `/admin` studio desk
- `/courier` rider desk (location is shared only while the rider turns it on)
