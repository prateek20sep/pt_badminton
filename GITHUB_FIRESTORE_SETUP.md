# 🚀 GitHub & Firestore Setup Guide

## Step 1: Push to GitHub

### 1.1 Create a GitHub Repository
1. Go to https://github.com/new
2. Create a new repository named `badminton-tournament`
3. Don't initialize with README (we have one)
4. Click "Create repository"

### 1.2 Push Your Code to GitHub

```bash
# Navigate to your project
cd /Users/prateekmishra/Documents/git_code/badminton-tournament

# Add remote origin (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/badminton-tournament.git

# Rename branch to main
git branch -M main

# Stage all changes
git add .

# Commit changes
git commit -m "Initial commit: Dynamic badminton tournament app with Firestore"

# Push to GitHub
git push -u origin main
```

---

## Step 2: Set Up Firestore Database

### 2.1 Create Firebase Project
1. Go to https://console.firebase.google.com
2. Click "Add project"
3. Name it "badminton-tournament"
4. Continue through the setup
5. Click "Create project"

### 2.2 Add Web App to Firebase
1. In Firebase Console, click "Add app"
2. Select "Web"
3. Name it "Badminton Tournament Web"
4. Check "Also set up Firebase Hosting for this app" (optional)
5. Click "Register app"
6. Copy the Firebase config (you'll need this)

### 2.3 Set Up Firestore Database
1. In Firebase Console, go to "Firestore Database"
2. Click "Create database"
3. Start in "Production mode"
4. Choose location (use closest to you)
5. Click "Create"

### 2.4 Set Up Firestore Security Rules
1. Go to "Firestore Database" → "Rules" tab
2. Replace the rules with:

```firestore
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      // Allow read/write for all users (for development)
      // TODO: Add proper authentication in production
      allow read, write: if true;
    }
  }
}
```

3. Click "Publish"

---

## Step 3: Configure Environment Variables

### 3.1 Get Firebase Credentials
1. Go to Firebase Console → Project Settings
2. Click "Your apps" section
3. Find your Web app
4. Click the "</>" icon to show config
5. Copy the config object

### 3.2 Create `.env.local` File
Create `.env.local` in your project root:

```bash
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_PROJECT.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_PROJECT.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_MESSAGING_SENDER_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

Example with actual values:
```bash
VITE_FIREBASE_API_KEY=AIzaSyDxGhTQ8Z_KpH8a4b9c1d2e3f4g5h6i7j8k
VITE_FIREBASE_AUTH_DOMAIN=badminton-tournament-123.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=badminton-tournament-123
VITE_FIREBASE_STORAGE_BUCKET=badminton-tournament-123.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=123456789012
VITE_FIREBASE_APP_ID=1:123456789012:web:abcdef1234567890
```

### 3.3 Add `.env.local` to `.gitignore`
Make sure `.env.local` is in `.gitignore` (it should already be):

```bash
# In .gitignore
.env.local
.env*.local
```

---

## Step 4: Test Firestore Connection

### 4.1 Start Development Server
```bash
npm run dev
```

### 4.2 Test in Browser
1. Open http://localhost:5173
2. Try adding a player
3. Check Firestore Console to see data appearing in `players` collection

---

## Step 5: Deploy to Firebase Hosting (Optional)

### 5.1 Install Firebase CLI
```bash
npm install -g firebase-tools
```

### 5.2 Initialize Firebase Hosting
```bash
firebase init hosting
```

Choose:
- Use existing project: Select your `badminton-tournament` project
- Public directory: `dist`
- SPA (rewrite URLs): Yes
- GitHub integration: Yes (optional)

### 5.3 Build for Production
```bash
npm run build
```

### 5.4 Deploy
```bash
firebase deploy
```

Your app will be live at: `https://YOUR_PROJECT.web.app`

---

## Step 6: Deploy to GitHub Pages (Alternative)

### 6.1 Update `vite.config.ts`
```typescript
export default {
  base: '/',
  // ... rest of config
}
```

### 6.2 Build
```bash
npm run build
```

### 6.3 Deploy to GitHub Pages
```bash
git add .
git commit -m "Build for production"
git push origin main
```

Then in GitHub:
1. Go to repository Settings
2. Click "Pages" on left sidebar
3. Set Source to "GitHub Actions"
4. Select "Node.js" workflow

---

## Firestore Database Structure

Your app will create these collections:

### `players` Collection
```
{
  id: (auto-generated)
  name: "Alice",
  email: "alice@example.com",
  phone: "+1234567890",
  rating: 1650,
  wins: 12,
  losses: 3,
  matchesPlayed: 15,
  createdAt: Date
}
```

### `tournaments` Collection
```
{
  id: (auto-generated)
  name: "Spring Championship",
  date: "2026-03-26",
  status: "in_progress",
  playerIds: [1, 2, 3, 4],
  format: "round_robin",
  createdAt: Date
}
```

### `matches` Collection
```
{
  id: (auto-generated)
  tournamentId: 1,
  player1Id: 1,
  player2Id: 2,
  player1Score: 21,
  player2Score: 18,
  winnerId: 1,
  status: "completed",
  round: 1,
  scheduledOrder: 1
}
```

### `standings` Collection
```
{
  id: (auto-generated)
  tournamentId: 1,
  playerId: 1,
  wins: 2,
  losses: 0,
  pointsFor: 42,
  pointsAgainst: 35
}
```

---

## Troubleshooting

### "Firebase config not found"
- Create `.env.local` with correct Firebase credentials
- Restart dev server after creating `.env.local`

### "Firestore permission denied"
- Check Firestore Rules are set to allow read/write
- Make sure database is in Production mode

### "Module not found: firebase"
```bash
npm install firebase
```

### "Firestore not updating"
- Check browser console for errors
- Verify Firebase config in `.env.local`
- Check Firestore Rules allow your operations

### "Data not appearing in Firestore Console"
- Wait a few seconds for sync
- Refresh Firestore Console
- Check browser console for errors

---

## Security Notes (For Production)

Before going live:

1. **Add Authentication**
   - Set up Firebase Auth
   - Update Firestore Rules to require authentication

2. **Secure Firestore Rules**
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

3. **Use Environment Variables**
   - Never commit `.env.local`
   - Always use `import.meta.env.VITE_*` for secrets

4. **Enable CORS if needed**
   - Firebase Hosting automatically handles CORS
   - Firestore handles CORS for authorized requests

---

## GitHub Repository Setup

### Add CI/CD (GitHub Actions)
Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Firebase

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18
      
      - name: Install dependencies
        run: npm install
      
      - name: Build
        run: npm run build
      
      - name: Deploy to Firebase
        uses: FirebaseExtended/action-hosting-deploy@v0
        with:
          repoToken: ${{ secrets.GITHUB_TOKEN }}
          firebaseServiceAccount: ${{ secrets.FIREBASE_SERVICE_ACCOUNT }}
          channelId: live
          projectId: YOUR_PROJECT_ID
```

---

## Next Steps

1. ✅ Create GitHub repository
2. ✅ Push code to GitHub
3. ✅ Create Firebase project
4. ✅ Set up Firestore
5. ✅ Configure `.env.local`
6. ✅ Test connection
7. ✅ Deploy to Firebase Hosting

**Your app is now cloud-ready!** 🚀

---

## Quick Commands Reference

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Deploy to Firebase
firebase deploy

# View Firebase logs
firebase functions:log

# Push to GitHub
git add .
git commit -m "Your message"
git push origin main
```

---

Need help? Check Firebase docs: https://firebase.google.com/docs

