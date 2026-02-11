# Bio_Ton

A GitHub Pages-based map viewer displaying Bio_O_Ton habitat suitability areas in the Saarland region of Germany.

## 🚀 Live Demo

Visit the interactive map: [https://fkistner85.github.io/Bio_Ton/](https://fkistner85.github.io/Bio_Ton/)

The map displays **64,321 habitat features** from the Bio_O_Ton project, showing habitat suitability areas in an interactive Leaflet map.

## 📖 What is This?

This repository hosts an interactive map viewer for the Bio_O_Ton project. Features:
- Display habitat suitability areas extracted from MBTiles
- Interactive map with clickable habitat features  
- Centered on Saarland, Germany (coordinates: 49.47°N, 6.5°E)
- GeoJSON overlay on OpenStreetMap base layer

## 📚 Documentation

- **[Quick Start Guide](docs/QUICKSTART.md)** - Get started in 5 minutes
- **[Setup Instructions](docs/SETUP.md)** - Detailed GitHub Pages setup
- **[Testing Guide](docs/TESTING.md)** - Verify your installation
- **[Format Guide](docs/FORMATS.md)** - Choose the right tile format
- **[Integration Examples](https://fkistner85.github.io/Bio_Ton/integration.html)** - Live code examples

## 🗺️ Using with umap

To use these tiles in umap:

1. Open your umap editor at [umap.openstreetmap.fr](https://umap.openstreetmap.fr)
2. Click on **"Edit settings"** (the layers icon)
3. Go to **"Change tile layers"** or **"Background"**
4. Select **"Add a custom layer"**
5. Enter the tile URL:
   ```
   https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
   ```
6. Adjust the attribution as needed
7. Save and view your custom tiles!

## 📦 Adding Your Own MBTiles

MBTiles files need to be extracted into individual tile files for GitHub Pages. Follow these steps:

### Step 1: Extract Tiles from MBTiles

Using `mbutil` (Python):
```bash
# Install mbutil
pip install mbutil

# Extract tiles
mb-util your-map.mbtiles docs/tiles/ --image_format=png
```

Using `tippecanoe` tile-join:
```bash
# Extract tiles
tile-join -e docs/tiles/ your-map.mbtiles
```

### Step 2: Commit and Push

```bash
git add docs/tiles/
git commit -m "Add custom map tiles"
git push
```

### Step 3: Enable GitHub Pages

1. Go to your repository settings
2. Navigate to **Pages**
3. Under **Source**, select **Deploy from a branch**
4. Select the `main` branch and `/docs` folder
5. Click **Save**

Your tiles will be available at: `https://[username].github.io/[repo]/tiles/{z}/{x}/{y}.png`

## 📁 Repository Structure

```
Bio_Ton/
├── docs/
│   ├── index.html          # Map viewer interface
│   └── tiles/              # Tile directory
│       └── [z]/[x]/[y].png # Tile pyramid structure
└── README.md
```

## 🔧 Tile Formats Supported

- **Raster tiles**: `.png`, `.jpg`, `.webp`
- **Vector tiles**: `.pbf` (with appropriate viewer setup)

## 📝 Notes

- GitHub Pages has a 1GB size limit per repository
- Individual files should be under 100MB
- For large tile sets, consider using a dedicated tile server or cloud storage
- Tiles are served statically, so no server-side processing is available

## 🤝 Integration Examples

### Leaflet.js
```javascript
L.tileLayer('https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png', {
    attribution: 'Bio Ton Tiles',
    maxZoom: 18
}).addTo(map);
```

### OpenLayers
```javascript
new ol.layer.Tile({
    source: new ol.source.XYZ({
        url: 'https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png'
    })
})
```

## 📄 License

This is a public repository for hosting map tiles. Please ensure your tiles comply with licensing requirements of the source data.

## 🆘 Troubleshooting

**Tiles not showing?**
- Verify GitHub Pages is enabled
- Check the tile URL pattern matches your directory structure
- Ensure tiles are in the correct format (PNG, JPG, etc.)
- Check browser console for CORS or 404 errors

**Attribution Requirements:**
- If using OpenStreetMap data, include: `© OpenStreetMap contributors`
- Add any other required attributions based on your data sources