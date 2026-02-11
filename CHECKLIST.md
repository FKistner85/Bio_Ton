# Action Checklist

Use this checklist to track your progress in setting up and using your GitHub Pages tile server.

## Phase 1: Initial Setup ✅ DONE

- [x] Repository structure created
- [x] Documentation files added
- [x] Map viewer interface created
- [x] Integration examples provided
- [x] Code committed and pushed

## Phase 2: Enable GitHub Pages 🎯 DO THIS NOW

- [ ] Go to repository Settings
- [ ] Navigate to Pages section
- [ ] Select source: `main` branch, `/docs` folder
- [ ] Save settings
- [ ] Wait 1-2 minutes for deployment
- [ ] Check deployment status (green badge in Pages settings)

## Phase 3: Verify Setup

- [ ] Visit https://fkistner85.github.io/Bio_Ton/
- [ ] Confirm map viewer loads
- [ ] Check info panel displays correctly
- [ ] Visit https://fkistner85.github.io/Bio_Ton/integration.html
- [ ] Confirm integration guide loads
- [ ] Test sample tile URL: https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.txt
- [ ] Open browser console (F12) and verify no errors

## Phase 4: Add Your Tiles (When Ready)

- [ ] Install mbutil: `pip install mbutil`
- [ ] Extract tiles: `mb-util your-map.mbtiles docs/tiles/ --image_format=png`
- [ ] Verify extracted structure: `docs/tiles/{z}/{x}/{y}.png`
- [ ] Commit tiles: `git add docs/tiles/`
- [ ] Push to GitHub: `git commit -m "Add tiles" && git push`
- [ ] Wait for GitHub Pages to redeploy (1-2 minutes)
- [ ] Test a real tile URL in browser

## Phase 5: Test Integration

### Test with umap
- [ ] Go to https://umap.openstreetmap.fr
- [ ] Create or open a map
- [ ] Add custom tile layer
- [ ] Enter URL: https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
- [ ] Verify tiles display correctly
- [ ] Adjust opacity if needed
- [ ] Save map

### Test with Leaflet (Optional)
- [ ] Create test HTML file with Leaflet
- [ ] Add tile layer with your URL
- [ ] Open in browser
- [ ] Verify tiles load
- [ ] Check network tab for 200 status codes

### Test with QGIS (Optional)
- [ ] Open QGIS
- [ ] Add XYZ tile layer
- [ ] Use your tile URL
- [ ] Verify tiles display

## Phase 6: Optimization (As Needed)

- [ ] Check total tile directory size: `du -sh docs/tiles/`
- [ ] Ensure under 1GB limit
- [ ] Optimize PNG files if needed: `optipng docs/tiles/**/*.png`
- [ ] Consider converting to JPEG for base maps
- [ ] Limit zoom levels to only what you need
- [ ] Remove unnecessary zoom levels

## Phase 7: Documentation

- [ ] Update README.md with specific attribution for your data
- [ ] Document the geographic extent of your tiles
- [ ] Note the zoom level range available
- [ ] Add any specific usage instructions
- [ ] Update tile format if not PNG

## Phase 8: Sharing

- [ ] Share tile URL with team/users
- [ ] Provide attribution requirements
- [ ] Document any usage restrictions
- [ ] Add examples specific to your use case

## Troubleshooting Checklist

If something doesn't work:

- [ ] GitHub Pages is enabled and showing "Active"
- [ ] Correct branch (`main`) and folder (`/docs`) selected
- [ ] All files committed and pushed
- [ ] Waited 1-2 minutes after changes
- [ ] Tried incognito/private window (clears cache)
- [ ] Checked browser console for errors
- [ ] Verified tile URL pattern matches directory structure
- [ ] Checked Actions tab for deployment errors
- [ ] Tile files are in correct format (.png, .jpg, etc.)
- [ ] File extensions in URL match actual files

## Quick Reference

### Tile URL Pattern
```
https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
```

### Update Tiles
```bash
mb-util new-tiles.mbtiles docs/tiles/ --image_format=png
git add docs/tiles/
git commit -m "Update tiles"
git push
```

### Check Size
```bash
du -sh docs/tiles/
```

### Test Tile
```bash
curl -I https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.png
```

## Status: Next Action Required

🎯 **YOUR NEXT STEP:** Enable GitHub Pages in Settings → Pages

After enabling Pages, work through the verification steps above.

---

**Need help?** See [SETUP_COMPLETE.md](SETUP_COMPLETE.md) for detailed instructions.
