# Quick Start Guide

## 🚀 Getting Started

This repository is ready to host MBTiles on GitHub Pages! Follow these quick steps:

### 1. Enable GitHub Pages

1. Go to **Settings** → **Pages** in your GitHub repository
2. Under **Source**, select:
   - Branch: `main`
   - Folder: `/docs`
3. Click **Save**
4. Wait 1-2 minutes for deployment

Your site will be live at: `https://fkistner85.github.io/Bio_Ton/`

### 2. Add Your Tiles

Extract your MBTiles and add them to the `docs/tiles/` directory:

```bash
# Install mbutil
pip install mbutil

# Extract your tiles
mb-util your-map.mbtiles docs/tiles/ --image_format=png

# Commit and push
git add docs/tiles/
git commit -m "Add map tiles"
git push
```

### 3. Use in umap

In umap, add a custom tile layer with this URL:
```
https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
```

## 📖 More Information

- Full documentation: See [README.md](../README.md)
- Setup instructions: See [SETUP.md](SETUP.md)
- Integration examples: Visit [integration.html](https://fkistner85.github.io/Bio_Ton/integration.html)

## 🔍 Verify Deployment

Once GitHub Pages is enabled, check:
- ✅ Main viewer: https://fkistner85.github.io/Bio_Ton/
- ✅ Integration guide: https://fkistner85.github.io/Bio_Ton/integration.html
- ✅ Tile access: https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.txt

## ⚡ Common Issues

**Site not loading?**
- Ensure Pages is enabled in Settings
- Check the correct branch and folder are selected
- Wait a few minutes for initial deployment

**Tiles showing 404?**
- Verify tile directory structure: `tiles/{z}/{x}/{y}.png`
- Check that tiles are committed and pushed
- Ensure file extensions match (.png, .jpg, etc.)

## 📞 Need Help?

Check the [SETUP.md](SETUP.md) file for detailed troubleshooting steps.
