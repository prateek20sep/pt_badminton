# 📋 GitHub & Firestore Quick Reference

## 🚀 3-Step Deployment

### Step 1: Create Firebase Project
```
1. Go to https://console.firebase.google.com
2. Click "Add project"
3. Name: badminton-tournament
4. Complete setup
5. Add Web app
6. Copy Firebase config
```

### Step 2: Set Up Environment
```bash
# Create .env.local with your Firebase config
VITE_FIREBASE_API_KEY=YOUR_API_KEY
VITE_FIREBASE_AUTH_DOMAIN=YOUR_DOMAIN
VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
VITE_FIREBASE_STORAGE_BUCKET=YOUR_BUCKET
VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_ID
VITE_FIREBASE_APP_ID=YOUR_APP_ID
```

### Step 3: Deploy
**Option A - Vercel (Easiest):**
```bash
git push origin main
# Then connect to Vercel at https://vercel.com
```

**Option B - Firebase:**
```bash
npm run firebase:deploy
```

**Option C - GitHub Pages:**
```bash
# Configure GitHub Actions (see .github/workflows/deploy.yml)
git push origin main
```

---

## 📁 What's New

| File | Purpose |
|------|---------|
| `src/lib/db-firestore.ts` | Firestore database wrapper |
| `.env.example` | Firebase config template |
| `GITHUB_FIRESTORE_SETUP.md` | Complete setup guide |
| `DEPLOYMENT.md` | Deployment guide |
| `README.md` | Updated project docs |

---

## 🔧 Key Commands

```bash
# Development
npm run dev              # Start dev server
npm run build           # Build for production

# Firebase
npm run firebase:deploy # Build & deploy to Firebase
firebase login         # Login to Firebase

# Git
git add .
git commit -m "message"
git push origin main
```

---

## 📊 Database Collections

**players** - Player information + ELO ratings
**tournaments** - Tournament details
**matches** - Match scores and results
**standings** - Tournament standings

---

## ✅ Deployment Checklist

- [ ] Firebase project created
- [ ] Firestore database set up
- [ ] .env.local configured locally
- [ ] Code pushed to GitHub
- [ ] Environment variables added to deployment platform
- [ ] Firestore Rules updated
- [ ] App tested
- [ ] Deployed

---

## 📚 Documentation

- **GITHUB_FIRESTORE_SETUP.md** - Start here
- **DEPLOYMENT.md** - Choose deployment method
- **README.md** - Project overview
- **.env.example** - Config template

---

## 🌐 Your App Will Be Live At

- **Vercel**: https://YOUR_PROJECT.vercel.app
- **Firebase**: https://YOUR_PROJECT.web.app  
- **GitHub Pages**: https://YOUR_USERNAME.github.io/badminton-tournament

---

**Need Help?** Check GITHUB_FIRESTORE_SETUP.md

