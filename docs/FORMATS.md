# Tile Format Guide

This guide explains the different tile formats you can use with this GitHub Pages setup.

## Supported Formats

### 1. Raster Tiles

#### PNG Tiles (Recommended)
- **Format:** `.png`
- **Pros:** Supports transparency, good quality, widely supported
- **Cons:** Larger file size than JPG
- **Best for:** Overlay tiles, tiles with transparency, maps with text
- **URL pattern:** `tiles/{z}/{x}/{y}.png`

**Example extraction:**
```bash
mb-util your-map.mbtiles docs/tiles/ --image_format=png
```

#### JPEG Tiles
- **Format:** `.jpg` or `.jpeg`
- **Pros:** Smaller file size, good for photos/satellite imagery
- **Cons:** No transparency support, lossy compression
- **Best for:** Satellite imagery, aerial photos, base maps without transparency
- **URL pattern:** `tiles/{z}/{x}/{y}.jpg`

**Example extraction:**
```bash
mb-util your-map.mbtiles docs/tiles/ --image_format=jpg
```

#### WebP Tiles
- **Format:** `.webp`
- **Pros:** Excellent compression, supports transparency
- **Cons:** Not supported in older browsers
- **Best for:** Modern web applications, need small file sizes
- **URL pattern:** `tiles/{z}/{x}/{y}.webp`

**Note:** Requires conversion tools that support WebP output.

### 2. Vector Tiles

#### PBF Tiles (Mapbox Vector Tiles)
- **Format:** `.pbf` or `.mvt`
- **Pros:** Very small file size, client-side rendering, dynamic styling
- **Cons:** Requires special viewer (MapLibre GL JS, Mapbox GL JS)
- **Best for:** Interactive maps with custom styling
- **URL pattern:** `tiles/{z}/{x}/{y}.pbf`

**Viewer requirement:** Use MapLibre GL JS or Mapbox GL JS instead of Leaflet.

## Tile Structure

All formats follow the same directory structure:
```
docs/tiles/
├── 0/           # Zoom level 0
│   └── 0/
│       └── 0.png
├── 1/           # Zoom level 1
│   ├── 0/
│   │   ├── 0.png
│   │   └── 1.png
│   └── 1/
│       ├── 0.png
│       └── 1.png
└── ...
```

## Choosing the Right Format

### For Base Maps (Full coverage)
**Recommended:** JPEG or WebP
- Smaller file sizes
- Better performance
- No transparency needed

### For Overlay Layers
**Recommended:** PNG
- Transparency support
- Can overlay on other maps
- Better for labels and annotations

### For Vector Data
**Recommended:** PBF
- Smallest file size
- Dynamic styling
- Smooth zooming

## File Size Considerations

### GitHub Pages Limits
- Repository size: 1GB recommended (hard limit: 1GB)
- Individual file size: 100MB recommended
- Total published site: 1GB

### Optimization Tips

1. **Choose appropriate zoom levels:**
   ```
   Zoom 0-5:   World to country level
   Zoom 6-10:  Regional level
   Zoom 11-14: City level
   Zoom 15-18: Street level
   Zoom 19+:   Building level
   ```

2. **Limit zoom range:**
   - Don't generate unnecessary zoom levels
   - Most uses only need zoom 0-16
   - Very detailed areas can go to zoom 18

3. **Compression:**
   ```bash
   # Optimize PNG tiles
   optipng -o7 tiles/**/*.png
   
   # Convert PNG to JPEG for base maps
   find tiles -name "*.png" -exec mogrify -format jpg {} \;
   ```

4. **Selective coverage:**
   - Only generate tiles for your area of interest
   - Use bounding box when extracting:
   ```bash
   mb-util --bbox="min_lon,min_lat,max_lon,max_lat" input.mbtiles output/
   ```

## Format Conversion

### PNG to JPEG
```bash
# Using ImageMagick
find tiles -name "*.png" -exec convert {} {}.jpg \;

# Using Python with Pillow
python -c "from PIL import Image; import glob
for f in glob.glob('tiles/**/*.png', recursive=True):
    Image.open(f).convert('RGB').save(f.replace('.png', '.jpg'), 'JPEG', quality=85)"
```

### PNG to WebP
```bash
# Using cwebp
find tiles -name "*.png" -exec cwebp {} -o {}.webp \;
```

## Using Different Formats in Code

### Leaflet with PNG
```javascript
L.tileLayer('https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png', {
    maxZoom: 18
}).addTo(map);
```

### Leaflet with JPEG
```javascript
L.tileLayer('https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.jpg', {
    maxZoom: 16
}).addTo(map);
```

### MapLibre with PBF (Vector Tiles)
```javascript
var map = new maplibregl.Map({
    container: 'map',
    style: {
        version: 8,
        sources: {
            'bio-ton': {
                type: 'vector',
                tiles: ['https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.pbf']
            }
        },
        layers: [/* your style layers */]
    }
});
```

## Metadata

MBTiles files contain metadata. After extraction, create a `metadata.json`:

```json
{
    "name": "Bio Ton Map",
    "description": "Custom map tiles for Bio Ton project",
    "version": "1.0.0",
    "format": "png",
    "type": "baselayer",
    "minzoom": 0,
    "maxzoom": 16,
    "bounds": [-180, -85, 180, 85],
    "center": [0, 0, 2],
    "attribution": "© Your Attribution"
}
```

Place this file in `docs/tiles/metadata.json` for reference.

## Testing Different Formats

To test if your format is working:

1. Check a tile directly in browser:
   ```
   https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.png
   ```

2. Verify MIME type in Network tab (F12):
   - PNG: `image/png`
   - JPEG: `image/jpeg`
   - WebP: `image/webp`
   - PBF: `application/x-protobuf`

3. Check file size:
   ```bash
   ls -lh docs/tiles/0/0/0.png
   ```

## Recommendations Summary

| Use Case | Format | Zoom Levels | Notes |
|----------|--------|-------------|-------|
| Satellite base map | JPEG | 0-16 | No transparency needed |
| Overlay with labels | PNG | 0-18 | Needs transparency |
| Modern web app | WebP | 0-16 | Best compression |
| Vector data | PBF | 0-14 | Requires MapLibre GL |
| Simple markers | PNG | 10-18 | For local details |

## Need Help?

- Check extraction tool documentation: `mb-util --help`
- Refer to MBTiles spec: https://github.com/mapbox/mbtiles-spec
- Leaflet docs: https://leafletjs.com
- MapLibre docs: https://maplibre.org
