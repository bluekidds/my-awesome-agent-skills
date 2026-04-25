# PDF Guide Reference

Use Python reportlab to generate a printable PDF pilgrimage guide.

## Setup

pip install reportlab --break-system-packages

## Page Structure

### Cover Page
- Anime title (large, centered)
- Subtitle: Pilgrimage Complete Guide
- Total number of locations and days
- Key location preview list

### Day Pages
For each day:
- Day header with theme name
- Route summary (Station A to Station B to ...)
- Each location card with: number, name (JP + local language), scene description, access info, duration, cost, tips

### Practical Info Page (Last page)
- Recommended transit passes (e.g., Tokyo Metro 24-hour pass)
- Best times to visit
- Weather considerations
- Photo credits and sources

## Code Pattern

Use SimpleDocTemplate with A4 pagesize, 20mm margins.
Use getSampleStyleSheet and add custom ParagraphStyles for SpotTitle and SceneDesc.
For colors, use HexColor from reportlab.lib.colors.

## CJK Font Handling

For Chinese/Japanese text in PDFs, use reportlab CID fonts:

from reportlab.pdfbase.cidfonts import UnicodeCIDFont
pdfmetrics.registerFont(UnicodeCIDFont('STSong-Light'))  # Chinese
pdfmetrics.registerFont(UnicodeCIDFont('HeiseiMin-W3'))   # Japanese

Or download and register Noto Sans CJK TTF font.

## QR Code for Google Maps Links

pip install qrcode pillow --break-system-packages

Use qrcode.make(url) to generate QR codes, save to BytesIO buffer, wrap with ImageReader for reportlab.

## Tips

- Use Spacer for vertical spacing between elements
- Use PageBreak between days
- Use Table with TableStyle for structured location info
- Set breakInside avoid for location cards
- Include page numbers in footer
