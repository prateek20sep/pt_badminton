# 🚀 Deployment Guide

This guide covers deploying your Badminton Tournament app to GitHub and Firebase Hosting.

## Option 1: GitHub + Vercel Deployment (Recommended)

### Step 1: Push to GitHub

```bash
cd /Users/prateekmishra/Documents/git_code/badminton-tournament

# Initialize git if not already done
git init

# Add your GitHub remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/badminton-tournament.git
git branch -M main

# Add all files
git add .

# Commit
git commit -m "Initial commit: Badminton tournament app with Firestore"

# Push to GitHub
git push -u origin main
```

### Step 2: Deploy to Vercel

1. Go to https://vercel.com
2. Click "New Project"
3. Import your GitHub repository
4. Set environment variables:
   ```
   VITE_FIREBASE_API_KEY=YOUR_API_KEY
   VITE_FIREBASE_AUTH_DOMAIN=YOUR_AUTH_DOMAIN
   VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
   VITE_FIREBASE_STORAGE_BUCKET=YOUR_STORAGE_BUCKET
   VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_ID
   VITE_FIREBASE_APP_ID=YOUR_APP_ID
   ```
5. Click "Deploy"

Your app will be live at `https://YOUR_PROJECT.vercel.app`

---

## Option 2: GitHub + Firebase Hosting

### Step 1: Push to GitHub (same as above)

### Step 2: Set Up Firebase Hosting

```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize Firebase in your project
firebase init hosting
```

Select:
- Use existing project: Choose your badminton-tournament project
- Public directory: `dist`
- Configure as single-page app: Yes
- GitHub integration: Yes

### Step 3: Configure Environment Variables in Firebase

1. Go to Firebase Console → Project Settings
2. Copy your Web app config
3. In your project, create `.env.local`:

```
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
VITE_FIREBASE_STORAGE_BUCKET=...
VITE_FIREBASE_MESSAGING_SENDER_ID=...
VITE_FIREBASE_APP_ID=...
```

### Step 4: Deploy

```bash
# Build the app
npm run build

# Deploy to Firebase
firebase deploy
```

Your app will be live at `https://YOUR_PROJECT.web.app`

---

## Option 3: GitHub Pages Deployment

### Step 1: Push to GitHub

### Step 2: Configure GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 18
      
      - name: Install dependencies
        run: npm install
      
      - name: Build
        env:
          VITE_FIREBASE_API_KEY: ${{ secrets.VITE_FIREBASE_API_KEY }}
          VITE_FIREBASE_AUTH_DOMAIN: ${{ secrets.VITE_FIREBASE_AUTH_DOMAIN }}
          VITE_FIREBASE_PROJECT_ID: ${{ secrets.VITE_FIREBASE_PROJECT_ID }}
          VITE_FIREBASE_STORAGE_BUCKET: ${{ secrets.VITE_FIREBASE_STORAGE_BUCKET }}
          VITE_FIREBASE_MESSAGING_SENDER_ID: ${{ secrets.VITE_FIREBASE_MESSAGING_SENDER_ID }}
          VITE_FIREBASE_APP_ID: ${{ secrets.VITE_FIREBASE_APP_ID }}
        run: npm run build
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          cname: badminton-tournament.dev  # Optional: use custom domain
```

### Step 3: Add Secrets to GitHub

1. Go to GitHub repository → Settings → Secrets and variables → Actions
2. Add these secrets:
   - `VITE_FIREBASE_API_KEY`
   - `VITE_FIREBASE_AUTH_DOMAIN`
   - `VITE_FIREBASE_PROJECT_ID`
   - `VITE_FIREBASE_STORAGE_BUCKET`
   - `VITE_FIREBASE_MESSAGING_SENDER_ID`
   - `VITE_FIREBASE_APP_ID`

### Step 4: Configure GitHub Pages

1. Go to Settings → Pages
2. Set "Source" to "GitHub Actions"
3. Your app will deploy automatically on every push to main

Your app will be live at `https://YOUR_USERNAME.github.io/badminton-tournament`

---

## Environment Variables Setup

### Firebase Console Configuration

1. Go to https://console.firebase.google.com
2. Select your project
3. Click "Project Settings" (gear icon)
4. Go to "Your apps" section
5. Find your Web app and click "</>"
6. Copy your config

Your config will look like:
```javascript
{
  apiKey: "AIzaSyDxGhTQ8Z_KpH8a4b9c1d2e3f4g5h6i7j8k",
  authDomain: "badminton-tournament-abc123.firebaseapp.com",
  projectId: "badminton-tournament-abc123",
  storageBucket: "badminton-tournament-abc123.appspot.com",
  messagingSenderId: "123456789012",
  appId: "1:123456789012:web:abcdef1234567890"
}
```

### Local Development

Create `.env.local` in project root:
```
VITE_FIREBASE_API_KEY=your_api_key_here
VITE_FIREBASE_AUTH_DOMAIN=your_domain.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_bucket.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

### Production Deployment

Set these environment variables in your deployment platform:
- **Vercel**: Project Settings → Environment Variables
- **Firebase Hosting**: `.env.production.local` or Firebase Console
- **GitHub Pages**: Repository Settings → Secrets and variables → Actions

---

## Quick Deployment Checklist

- [ ] Code pushed to GitHub
- [ ] Firebase project created
- [ ] Firestore database set up
- [ ] Environment variables configured
- [ ] `.env.local` created locally
- [ ] GitHub secrets added (if using GitHub Actions)
- [ ] Firestore Rules updated (allow/deny based on needs)
- [ ] App tested in development
- [ ] npm run build works
- [ ] Deployed successfully
- [ ] Testing in production environment

---

## Firestore Security Setup

### For Development (allows all):
```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

### For Production with Auth:
```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

### For Public Read, Authenticated Write:
```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

---

## Commands Reference

```bash
# Development
npm run dev                    # Start dev server
npm run build                 # Build for production
npm run preview               # Preview production build

# Deployment
npm run firebase:deploy       # Build and deploy to Firebase
firebase deploy --only hosting  # Deploy only hosting (if Realtime DB set up)

# Git
git status                    # Check git status
git add .                     # Stage all files
git commit -m "message"       # Commit changes
git push origin main          # Push to GitHub

# Firebase
firebase init hosting         # Initialize Firebase hosting
firebase login               # Login to Firebase
firebase serve               # Test Firebase locally
firebase emulators:start     # Start local emulators
```

---

## Troubleshooting Deployment

### Build Fails with "Firebase config not found"
```
Solution: Create .env.local with Firebase credentials
Restart dev server with: npm run dev
```

### Deployment succeeds but app shows errors
```
Solution: Check browser console for errors
Verify Firebase credentials in deployed environment
Check Firestore Rules allow your operations
```

### "Cannot find module 'firebase'"
```
Solution: npm install firebase
Rebuild: npm run build
```

### Firestore operations fail in production
```
Solution: Update Firestore Rules to allow your operations
Check authentication is set up if required
Verify database location matches project
```

### Environment variables not loading
```
Solution for Vercel: Settings → Environment Variables
Solution for Firebase: Set in .env.production.local
Solution for GitHub Pages: Add secrets in repository settings
```

---

## Post-Deployment

1. **Test All Features**
   - Add players
   - Create tournaments
   - Score matches
   - Check leaderboard

2. **Monitor Performance**
   - Check Firebase Console → Firestore usage
   - Monitor Hosting metrics

3. **Update DNS** (if using custom domain)
   - Configure your domain registrar
   - Point to your hosting service

4. **Set Up CI/CD**
   - GitHub Actions for automatic deployments
   - Deploy on every push to main

5. **Backup Data**
   - Enable Firestore backups
   - Export data regularly

---

## Support

- Firebase Docs: https://firebase.google.com/docs
- Vercel Docs: https://vercel.com/docs
- GitHub Pages: https://pages.github.com
- GitHub Actions: https://github.com/features/actions

---

Happy Deploying! 🚀

