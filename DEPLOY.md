# GitHub Pages Deployment Guide

## Changes Made for PWA and GitHub Pages

### 1. PWA Configuration
- ✅ Created `public/service-worker.js` for offline caching
- ✅ Updated `public/manifest.json` with proper PWA settings
- ✅ Added service worker registration in `src/client/index.tsx`
- ✅ Fixed service worker path for GitHub Pages
- ✅ Created `public/.nojekyll` to prevent Jekyll processing

### 2. GitHub Pages Configuration
- ✅ Updated `package.json` homepage to GitHub Pages URL
- ✅ Added deploy scripts to `package.json`
- ✅ Updated webpack config with `/takenote/` base path
- ✅ Updated router history with basename for production
- ✅ Updated canonical URL in App.tsx
- ✅ Created GitHub Actions workflow (`.github/workflows/deploy.yml`)
- ✅ Removed landing page - app loads directly

### 3. GitHub Actions Workflows

**Why you see 2 workflow runs:**

1. **"Deploy to GitHub Pages"** - Our custom workflow that:
   - Builds the app with webpack
   - Pushes to `gh-pages` branch

2. **"pages build and deployment"** - GitHub's automatic workflow that:
   - Deploys the `gh-pages` branch to GitHub Pages
   - Runs automatically after our workflow

This is **normal and expected**. Both are needed for the deployment to work.

### 4. Manual Deployment Steps

Since npm install has issues with node-sass, use manual deployment:

```bash
# 1. Build the project (if dependencies are already installed)
npm run build

# 2. Deploy to GitHub Pages manually
npx gh-pages -d dist
```

### 5. GitHub Repository Setup

1. Go to your GitHub repository settings
2. Navigate to Pages section
3. Set source to `gh-pages` branch
4. Your app will be available at: `https://Paresh-Maheshwari.github.io/takenote`

### 6. Automatic Deployment

The GitHub Actions workflow automatically deploys on push to master branch.
Make sure GitHub Actions is enabled in your repository settings.

### 7. Testing PWA Features

After deployment:
- Open the app in Chrome/Edge
- Check DevTools > Application > Service Workers (should show active)
- Check DevTools > Application > Manifest
- Try "Add to Home Screen" option
- Test offline functionality

### 8. Important Notes

- The app runs in DEMO mode (no GitHub OAuth)
- All notes are stored in browser localStorage
- Service worker caches the app for offline use
- Base path is `/takenote/` for GitHub Pages
- App loads directly without landing page

### 9. Troubleshooting

If the app doesn't load:
- Check browser console for errors
- Verify the base path in URLs
- Clear browser cache and service workers
- Check GitHub Pages settings

If service worker fails:
- Check that service-worker.js is accessible at `/takenote/service-worker.js`
- Clear old service workers in DevTools > Application > Service Workers

### Files Modified:
- `package.json` - Added homepage, deploy scripts
- `config/webpack.common.js` - Added publicPath for production
- `src/client/index.tsx` - Added service worker registration
- `src/client/serviceWorker.ts` - Fixed path for GitHub Pages
- `src/client/utils/history.ts` - Added basename
- `src/client/containers/App.tsx` - Updated canonical URL, removed landing page
- `public/manifest.json` - Updated start_url
- `public/service-worker.js` - Created
- `public/.nojekyll` - Created
- `.github/workflows/deploy.yml` - Created
