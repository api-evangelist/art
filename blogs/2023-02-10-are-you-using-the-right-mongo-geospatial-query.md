---
title: "Are you using the right Mongo geospatial query?"
url: "https://artsy.github.io/blog/2023/02/10/mongo-geospatial-queries/"
date: "2023-02-10"
feed_url: "https://artsy.github.io/feed"
---
We recently got a report from one of our galleries in the Los Angeles area that they weren’t showing up on our Los Angeles exhibition listings . I fielded the report and right away confirmed: when we asked our core API for /shows?near= , sure enough this gallery partner didn’t make the cut. Turns out they are based in Santa Monica, a separate and neighboring municipality.
