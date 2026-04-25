# Anubis — Privacy Policy

_Last updated: 2026-04-25_

Anubis is a Chrome extension that builds a crowd-sourced price-history chart
for AliExpress products. This document describes exactly what data the
extension transmits, why, where it goes, and what is **not** collected.

## What Anubis sends

When you visit a product page on AliExpress (and only those pages), Anubis
extracts and transmits the following fields to the server at
`https://anubisprice.duckdns.org`:

- AliExpress product ID (numeric, from the URL)
- Product title (as shown on the page)
- Price and currency (as shown on the page)
- Shipping cost (as shown on the page, if any)
- Selected variant attributes (e.g. `Color: White`, `Size: M`)
- The product page URL with all query-string and hash fragments removed
  (e.g. `https://he.aliexpress.com/item/1005010599100890.html` — never the
  `?spm=…` / `?pdp_ext_f=…` tracking parameters)
- The page domain (e.g. `he.aliexpress.com`)
- The page language code (e.g. `en`, `he`)
- An anonymous install identifier — a random UUID generated the first time
  the extension runs and stored locally in your browser. It is **not** linked
  to your Google account, IP, name, or any other identity.

When you open the price-history panel, the extension additionally sends the
product ID, domain, currency, and selected variant key to fetch matching
history. No other data is included in history requests.

## What Anubis does NOT collect

- Your name, email, phone number, or Google account
- Your AliExpress account, login credentials, or order history
- Payment information of any kind
- Pages outside `*.aliexpress.*` domains
- The URLs of non-product pages (search results, your cart, etc.)
- Browsing data when you are not logged into AliExpress (the extension
  intentionally skips data extraction on non-logged-in views)
- Cookies, local storage, or session tokens
- Mouse movements, keystrokes, screen recordings, or analytics events

## Server-side handling

Submitted observations are stored in a PostgreSQL database with the fields
listed above plus a server-assigned timestamp. Server logs retain the
request method, request path (without query string), a salted truncated
hash of the client IP, and the install identifier prefix. The salt rotates
on every server restart, so log entries cannot be linked back to an IP
address after a restart and cannot be joined across deployments.

The server is operated by the extension author on personal infrastructure
located in Israel. No third-party analytics, advertising, or tracking
services receive any data.

## Data sharing

Aggregated price history is returned to other Anubis users when they view
the same product. Individual observations are not attributable to a
specific user, install, or IP in this returned history.

No data is sold, rented, or otherwise disclosed to third parties.

## Your choices

- To stop all data collection, uninstall the extension. All locally stored
  state (including the install identifier) is removed when Chrome
  uninstalls the extension.
- To request deletion of historical data associated with your install
  identifier, contact the address below with the UUID. You can find it in
  Chrome DevTools → Application → Storage → Extension storage →
  `anubis_install_id`.

## Contact

For questions or data-deletion requests, contact:
`pavelgurwitz@gmail.com`

## Changes

Material changes to this policy will be published in the extension's release
notes and at the top of this document.
