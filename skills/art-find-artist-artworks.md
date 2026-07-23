---
name: Find an artist and browse their artworks on Artsy
description: Authenticate with an XApp token, search for an artist by name, then page through that artist's artworks.
api: openapi/art-openapi.yml
operations: [createXappToken, search, listArtists, getArtist, listArtworks]
---

# Find an artist and browse their artworks

Use the Artsy Public API (v2) to look up an artist and list their artworks. All requests go to
`https://api.artsy.net/api`.

## 1. Mint an XApp token (`createXappToken`)
`POST /tokens/xapp_token` with `client_id` and `client_secret` (form-urlencoded). The response
returns `token` and `expires_at`. Send `X-Xapp-Token: <token>` on every subsequent request.

## 2. Find the artist (`search` or `listArtists`)
- Broad: `GET /search?q=<name>` (full-text across resources), or
- Targeted: `GET /artists?term=<name>`.
Take the artist `id` from the matching result's `_links.self`.

## 3. Confirm the artist (`getArtist`)
`GET /artists/{id}` to read the artist record.

## 4. List the artworks (`listArtworks`)
`GET /artworks?artist_id={id}&size=25&total_count=1`. Follow `_links.next` to page (cursor-based);
do not combine `cursor` with `offset`.

## Rules
- Rate limit: 5 requests/second per application ID — back off on HTTP 429.
- Errors are `{type,message,detail}`; `auth_error` means refresh the token.
- `total_count` is only present when you pass `total_count=1`, and is approximate.
