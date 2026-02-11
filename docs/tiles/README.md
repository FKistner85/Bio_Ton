# Tiles Directory

This directory is for hosting your tile pyramid extracted from MBTiles.

## How to Add Your MBTiles

MBTiles is a SQLite database format for storing map tiles. To host tiles on GitHub Pages (which is a static file server), you need to extract the tiles from the MBTiles file into a directory structure.

### Extracting Tiles from MBTiles

You can use tools like `mb-util` to extract tiles:

```bash
# Install mb-util (requires Python)
pip install mbutil

# Extract tiles from your MBTiles file
mb-util your-tiles.mbtiles tiles/ --image_format=png
```

Or use `tile-join` from Mapbox's tippecanoe:

```bash
# Extract tiles
tile-join -e tiles/ your-tiles.mbtiles
```

### Expected Directory Structure

After extraction, your tiles should be organized as:
```
tiles/
├── 0/
│   └── 0/
│       └── 0.png
├── 1/
│   └── 0/
│       ├── 0.png
│       └── 1.png
├── ...
└── [zoom]/[x]/[y].png
```

### For Testing

A sample tile has been provided in this directory to demonstrate the structure.

## Using with OpenStreetMap/umap

Once your tiles are hosted, use the following URL pattern in umap:
```
https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
```

Replace `.png` with `.jpg`, `.webp`, or `.pbf` depending on your tile format.
