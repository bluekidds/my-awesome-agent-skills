---
name: anime-pilgrimage
description: >
  Create interactive anime pilgrimage travel guides with real-location maps,
  anime-vs-reality photo comparisons, and multi-day itineraries. Use this skill whenever
  the user mentions: pilgrimage guide, anime locations, real-life anime spots,
  filming locations for anime, seichi junrei, location scouting for any anime/movie,
  anime travel itinerary, or wants to visit places from an anime. Supports output as
  interactive HTML (with Leaflet maps and comparison sliders), PDF print guide, and PPTX.
---

# Anime Pilgrimage Guide Creator

Build beautiful, interactive pilgrimage guides for any anime. This skill turns an anime title into a complete travel guide with maps, anime-vs-reality photo comparisons, and optimized multi-day itineraries.

## Workflow Overview

1. RESEARCH -> 2. IMAGE SOURCING -> 3. ROUTE PLANNING -> 4. BUILD OUTPUTS

## Step 1: Research Locations

Search for pilgrimage locations using these query patterns (try both Japanese and English):

- Japanese: "[title] seichi junrei location all spots"
- English: "[anime name] real life locations pilgrimage complete guide"

Key data to collect for each location:
- Name (Japanese + English/Chinese)
- GPS coordinates (latitude, longitude)
- Which scene it corresponds to
- Nearest station and walking time
- Whether the location still exists or has changed
- Admission fee if applicable
- Recommended visit duration

### Recommended Source Sites

- astral-tanbou.com - Detailed comparison photos with anime screenshots
- seichimap.jp - Structured pilgrimage maps
- thegate12.com - Well-organized location guides
- seichi-junrei.info - Fan community pilgrimage spots
- animepilgrimage.com - Multi-language with map pins

## Step 2: Image Sourcing

### Finding Comparison Photos

Search for anime-vs-reality comparison photos using Japanese and English queries.

### Extracting Images from Pilgrimage Blogs

When you find a blog with comparison photos, use Chrome browser tools to:
1. Navigate to the blog post
2. Use JavaScript to extract all image URLs with their surrounding text context
3. Cross-reference text context with locations to build correct mapping

CRITICAL: Verify image-location mapping. Blog images are ordered by the blog narrative, NOT by location. Always cross-reference surrounding text context with the location you are assigning the image to.

### Handling Hotlink Protection

Many Japanese CDNs block hotlinking via the Referer header. Two essential fixes:

1. Add to head: <meta name="referrer" content="no-referrer">
2. Add to every img tag: referrerpolicy="no-referrer"

If images still don't load:
- Navigate directly to each image URL in Chrome
- Use canvas to convert to base64 (same-origin works when navigating directly)
- Or use screenshot with save_to_disk to capture locally

## Step 3: Route Planning

### Geographic Clustering

1. Plot all coordinates on a map
2. Cluster nearby locations (within walking distance or 1-2 train stops)
3. Create a logical walking/transit route within each cluster
4. Assign clusters to days, ordered by geographic flow

Each day should have:
- A thematic name reflecting the anime story arc
- 4-6 locations maximum
- A meal recommendation for the area
- Total estimated time including transit

## Step 4: Build Outputs

### Output A: Interactive HTML

Use Leaflet.js for maps (no API key needed), photo comparison sliders, anime-themed visual effects, and day navigation tabs. See references/html-template.md for full code patterns.

### Output B: PDF Guide

Use Python reportlab for printable guides. See references/pdf-guide.md for structure and CJK font handling.

### Output C: PPTX Presentation

Use the pptx skill for visual presentations with comparison photos.

## Quality Checklist

- All images load correctly (check referrer policy)
- Each image matches its labeled location
- Map markers are at correct GPS coordinates
- Day routes make geographic sense (no backtracking)
- Google Maps links point to right locations
- Demolished/changed locations are noted
- Photo credits are included
- Mobile-responsive design works
