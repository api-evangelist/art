---
name: Browse Artsy genes and current shows
description: Use the Art Genome Project genes and the shows resource to discover artworks by category and find current gallery/museum shows.
api: openapi/art-openapi.yml
operations: [createXappToken, listGenes, getGene, listShows, listArtworks]
---

# Browse genes and shows

## 1. Authenticate (`createXappToken`)
Mint an `X-Xapp-Token` as in the find-artist skill.

## 2. Explore genes (`listGenes` / `getGene`)
`GET /genes` lists Art Genome Project genes (Artsy's classification of artistic characteristics).
`GET /genes/{id}` reads one. Filter genes for an artist with `GET /genes?artist_id={id}` or for an
artwork with `GET /genes?artwork_id={id}`.

## 3. Find shows (`listShows`)
`GET /shows?status=current` lists current shows. Filter by partner with `partner_id` or by fair
with `fair_id`. Read a show with `GET /shows/{id}`.

## 4. Pull a show's artworks (`listArtworks`)
`GET /artworks?show_id={id}&size=25`. Page via `_links.next`.

## Rules
- Same auth, rate limit (5 req/s), pagination and error semantics as the other Artsy skills.
- Resources are HAL: follow `_links` rather than constructing URLs by hand where possible.
