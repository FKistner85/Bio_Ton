# Testing and Verification Guide

This guide helps you test and verify your GitHub Pages tile server setup.

## Prerequisites

Before testing, ensure:
- [x] All files are committed and pushed to GitHub
- [x] GitHub Pages is enabled (Settings → Pages → Source: `main` branch, `/docs` folder)
- [ ] Wait 1-2 minutes after enabling Pages for deployment

## Step 1: Enable GitHub Pages

If you haven't already:

1. Go to your repository on GitHub: `https://github.com/FKistner85/Bio_Ton`
2. Click **Settings** (top menu)
3. Click **Pages** (left sidebar)
4. Under **Source**:
   - Select branch: `main`
   - Select folder: `/docs`
5. Click **Save**
6. Wait for the green banner: "Your site is published at..."

## Step 2: Verify Main Page

### Test 1: Homepage Load
1. Visit: `https://fkistner85.github.io/Bio_Ton/`
2. You should see:
   - ✅ A full-screen map (Leaflet)
   - ✅ An info panel on the right with instructions
   - ✅ OpenStreetMap base layer displayed

**If it doesn't work:**
- Check browser console (F12) for errors
- Verify Pages deployment status in Settings → Pages
- Check Actions tab for any deployment errors

### Test 2: Integration Guide
1. Visit: `https://fkistner85.github.io/Bio_Ton/integration.html`
2. You should see:
   - ✅ Comprehensive integration documentation
   - ✅ Code examples for Leaflet, OpenLayers
   - ✅ Step-by-step umap instructions

## Step 3: Test Tile Access

### Test 3: Sample Tile Access
Try accessing the sample tile:
```
https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.txt
```

**Expected result:** Should download or display the placeholder text file

### Test 4: Directory Listing (Optional)
Some setups show directory listings:
```
https://fkistner85.github.io/Bio_Ton/tiles/0/0/
```

**Expected result:** May show index.html or file listing

## Step 4: Add Real Tiles (When Ready)

### Extract and Add Tiles
```bash
# Install extraction tool
pip install mbutil

# Extract your MBTiles
mb-util your-map.mbtiles docs/tiles/ --image_format=png

# Commit and push
git add docs/tiles/
git commit -m "Add actual map tiles"
git push
```

### Test 5: Verify Real Tiles
After adding real tiles, test a specific tile:
```
https://fkistner85.github.io/Bio_Ton/tiles/[Z]/[X]/[Y].png
```

Replace `[Z]`, `[X]`, `[Y]` with actual coordinates from your tileset.

**Common zoom level 0 tile:**
```
https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.png
```

## Step 5: Test in umap

### Test 6: umap Integration
1. Go to: `https://umap.openstreetmap.fr`
2. Create a new map or open existing
3. Click the layers icon
4. Select "Add a remote layer" or "Custom layer"
5. Enter tile URL: `https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png`
6. Set name: "Bio Ton Tiles"
7. Save and zoom to your tile area

**Expected result:** Your tiles should appear on the map

**Troubleshooting:**
- If tiles don't show, check browser console
- Verify the zoom level has tiles available
- Check network tab (F12) for 404 errors

## Step 6: Test in Leaflet (Local)

Create a test HTML file:

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
    <style>#map { height: 500px; }</style>
</head>
<body>
    <div id="map"></div>
    <script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
    <script>
        var map = L.map('map').setView([0, 0], 2);
        L.tileLayer('https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png', {
            attribution: 'Bio Ton Tiles',
            maxZoom: 18
        }).addTo(map);
    </script>
</body>
</html>
```

Open in browser and verify tiles load.

## Common Issues and Solutions

### Issue: 404 Not Found
**Symptoms:** Tiles return 404 errors

**Solutions:**
1. Verify file structure: `tiles/{z}/{x}/{y}.png`
2. Check files are committed and pushed
3. Wait for GitHub Pages to deploy (1-2 minutes)
4. Verify Pages is enabled in Settings

### Issue: Blank/Empty Tiles
**Symptoms:** Map loads but tiles are blank

**Solutions:**
1. Check if zoom level has available tiles
2. Verify tile coordinates are correct
3. Ensure tiles extracted properly from MBTiles
4. Check file format matches URL (.png, .jpg, etc.)

### Issue: CORS Errors
**Symptoms:** Console shows CORS policy errors

**Solutions:**
1. GitHub Pages should handle CORS automatically
2. Verify you're accessing via HTTPS
3. Check that Pages is properly enabled
4. Try clearing browser cache

### Issue: Map Not Loading
**Symptoms:** Blank page or map container

**Solutions:**
1. Check browser console for JavaScript errors
2. Verify Leaflet CDN is accessible
3. Check network tab for failed resource loads
4. Try a different browser

### Issue: Slow Loading
**Symptoms:** Tiles load very slowly

**Solutions:**
1. Large tiles take time to load
2. Consider optimizing tile size
3. Reduce tile file sizes with compression
4. Use appropriate zoom levels

## Performance Testing

### Check Tile Size
```bash
# Check individual tile sizes
ls -lh docs/tiles/[z]/[x]/[y].png

# Check total directory size
du -sh docs/tiles/
```

**Recommendations:**
- Individual tiles: < 50KB ideal, < 200KB acceptable
- Total size: < 500MB (GitHub Pages limit is 1GB per repo)

### Load Time Test
1. Open browser DevTools (F12)
2. Go to Network tab
3. Load your page
4. Check tile load times
5. Aim for < 500ms per tile

## Verification Checklist

Before considering setup complete:

- [ ] GitHub Pages enabled and deployed
- [ ] Homepage loads without errors
- [ ] Integration guide is accessible
- [ ] Sample tile structure is in place
- [ ] Documentation is clear and complete
- [ ] README has correct repository URL
- [ ] Tile URL pattern is documented
- [ ] Attribution requirements noted
- [ ] At least one test tile added (when available)
- [ ] Tested in umap successfully (if tiles available)
- [ ] No console errors on homepage
- [ ] Mobile responsive (test on phone)

## Next Steps

After verification:
1. Add your actual MBTiles
2. Test with real data
3. Document your specific tile coverage area
4. Update attribution if using third-party data
5. Share your tile URL with collaborators

## Support

If you encounter issues:
1. Check GitHub Actions deployment logs
2. Review browser console errors
3. Verify all files are committed
4. Check GitHub Pages documentation
5. Refer to SETUP.md for detailed instructions

---

**Pro Tip:** Use browser DevTools Network tab to inspect tile requests and responses. This helps identify issues with tile loading.
