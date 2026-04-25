# HTML Template Reference

Proven HTML/CSS/JS patterns for building interactive pilgrimage guides.

## Page Structure

Use this base HTML structure with Leaflet.js for maps and Noto Sans TC for CJK text:

- DOCTYPE html with lang attribute matching user language
- meta charset UTF-8, viewport for mobile, referrer no-referrer
- Leaflet CSS and JS from cdnjs.cloudflare.com/ajax/libs/leaflet/1.9.4/
- Google Fonts Noto Sans TC

## CSS Components

### Core Layout
- Body: gradient background matching anime mood, Noto Sans TC font family
- Cards: rgba(255,255,255,0.92) background, 16px border-radius, hover lift effect
- Spot headers: gradient background with spot number circle, name, and badge

### Photo Comparison Slider

Structure: container with two sides (anime/real), a draggable divider, and labels.

- .comparison-container: relative position, 16:9 aspect ratio, overflow hidden, cursor col-resize
- .comparison-side: absolute positioned, 50% width each
- .comparison-side img: width/height 100%, object-fit cover
- .comparison-divider: 4px white bar at 50% left, with circle handle at center
- .comparison-label: absolute bottom badges showing "anime" and "real"

JavaScript: mousedown/touchstart on container starts dragging, mousemove/touchmove updates divider left% and anime side width%, mouseup/touchend stops.

### Map Integration (Leaflet.js)

No API key needed. Use OpenStreetMap tiles:
- Tile URL: https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png
- Custom numbered markers using L.divIcon with gold circle styling
- Route polyline with dashed gold line connecting spots
- map.fitBounds with padding for auto-zoom
- scrollWheelZoom disabled for better UX
- Lazy-init maps for non-active day tabs

### Day Navigation

Sticky tab bar at top. Each tab switches day section visibility.
After showing a day, call map.invalidateSize() to fix rendering.

### Particle Effects

Match to anime mood:
- Rain: vertical falling drops with gradient transparency (Weathering With You)
- Cherry blossoms: floating/swaying petals (5 Centimeters Per Second)
- Comet sparkles: glowing particles (Your Name)
- Stars/fireflies: gentle floating lights (Suzume)

Add a toggle button (fixed top-right) to switch effects on/off.

## Anime Theme Presets

| Anime | Colors | Effect |
|-------|--------|--------|
| Weathering With You | Blue sky + gold | Rain/sunshine toggle |
| Your Name | Twilight purple + orange | Comet sparkles |
| Suzume | Warm earth + sunset | Stars/butterflies |
| 5cm Per Second | Soft pink + gray | Cherry blossom petals |
| Garden of Words | Green + rain gray | Rain drops |

## Info Grid Pattern

Each spot card has an info grid with:
- Access info (station + walk time) with train emoji
- Suggested duration with clock emoji
- Cost with money emoji
- Tips with lightbulb emoji

Plus a Google Maps link button: maps.google.com/?q=LAT,LNG

## Print Styles

Hide particle effects, weather toggle, scroll hints.
Set body background to white, cards to break-inside avoid.
Make day-nav position relative instead of sticky.
