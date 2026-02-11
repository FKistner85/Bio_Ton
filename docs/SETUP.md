# GitHub Pages Setup for Bio_Ton

This file provides instructions for enabling GitHub Pages for this repository.

## Method 1: Using Repository Settings (Recommended)

1. Go to your repository on GitHub: `https://github.com/FKistner85/Bio_Ton`
2. Click on **Settings** tab
3. Scroll down to **Pages** section in the left sidebar
4. Under **Source**, select:
   - Branch: `main` (or your default branch)
   - Folder: `/docs`
5. Click **Save**
6. Wait a few minutes for deployment
7. Your site will be available at: `https://fkistner85.github.io/Bio_Ton/`

## Method 2: Using GitHub Actions (Alternative)

If you prefer using GitHub Actions for deployment, you can use the workflow below.

## Deployment Status

After enabling GitHub Pages, you can check deployment status:
- Go to **Actions** tab in your repository
- Look for "pages-build-deployment" workflow runs
- Each push to the `main` branch will trigger a new deployment

## Custom Domain (Optional)

To use a custom domain:
1. Add a `CNAME` file in the `docs/` directory with your domain name
2. Configure DNS settings with your domain provider
3. Update the domain in GitHub Pages settings

## CORS Configuration

GitHub Pages automatically serves files with appropriate CORS headers for tile serving. No additional configuration needed.

## Tile URL Format

Once deployed, your tiles will be accessible at:
```
https://fkistner85.github.io/Bio_Ton/tiles/{z}/{x}/{y}.png
```

Replace the zoom `{z}`, x-coordinate `{x}`, and y-coordinate `{y}` with actual values, or use this pattern in mapping libraries.

## Verification

To verify your setup is working:
1. Visit: `https://fkistner85.github.io/Bio_Ton/`
2. You should see the map viewer interface
3. Check browser console for any errors
4. Try accessing a tile directly: `https://fkistner85.github.io/Bio_Ton/tiles/0/0/0.png`

## Troubleshooting

**404 Errors:**
- Ensure the branch and folder are correctly set in Pages settings
- Verify files are committed and pushed to the repository
- Wait a few minutes after making changes for deployment to complete

**Tiles Not Loading:**
- Check the tile directory structure matches: `tiles/{z}/{x}/{y}.png`
- Verify image files are in the correct format
- Check browser console for CORS or network errors

**Deployment Failed:**
- Check the Actions tab for error logs
- Ensure all file sizes are within GitHub's limits
- Verify repository is public (or Pages is enabled for private repos)
