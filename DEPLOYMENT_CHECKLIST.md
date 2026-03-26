# ✅ Deployment Checklist

## Pre-Deployment Verification

### Code Quality
- [ ] npm run build completes without errors
- [ ] npm run type-check passes
- [ ] No console errors in dev mode
- [ ] All features work locally

### Firebase Setup
- [ ] Firebase project created
- [ ] Web app added to Firebase
- [ ] Firestore database created
- [ ] Firebase config copied

### Environment
- [ ] .env.local created with Firebase credentials
- [ ] .env.local is in .gitignore
- [ ] All 6 Firebase variables set
- [ ] npm run dev works with .env.local

### Git
- [ ] Repository initialized
- [ ] All files added to git
- [ ] Initial commit done
- [ ] Remote origin configured

---

## Deployment Steps (Choose ONE)

### Option A: Vercel Deployment ⭐
- [ ] Visit https://vercel.com
- [ ] Sign up/login with GitHub
- [ ] Import repository
- [ ] Add environment variables:
  - [ ] VITE_FIREBASE_API_KEY
  - [ ] VITE_FIREBASE_AUTH_DOMAIN
  - [ ] VITE_FIREBASE_PROJECT_ID
  - [ ] VITE_FIREBASE_STORAGE_BUCKET
  - [ ] VITE_FIREBASE_MESSAGING_SENDER_ID
  - [ ] VITE_FIREBASE_APP_ID
- [ ] Click Deploy
- [ ] Wait for build to complete
- [ ] Visit your app URL

**Your URL:** https://YOUR_PROJECT.vercel.app

---

### Option B: Firebase Hosting
- [ ] Install Firebase CLI: `npm install -g firebase-tools`
- [ ] Login: `firebase login`
- [ ] Initialize: `firebase init hosting`
- [ ] Build: `npm run build`
- [ ] Deploy: `firebase deploy`
- [ ] Check: `https://YOUR_PROJECT.web.app`

**Your URL:** https://YOUR_PROJECT.web.app

---

### Option C: GitHub Pages
- [ ] Create `.github/workflows/deploy.yml`
- [ ] Add GitHub secrets (6 Firebase vars)
- [ ] Push to main branch
- [ ] Wait for GitHub Actions
- [ ] Check: `https://YOUR_USERNAME.github.io/badminton-tournament`

**Your URL:** https://YOUR_USERNAME.github.io/badminton-tournament

---

## Post-Deployment Testing

### App Loads
- [ ] App loads without errors
- [ ] UI displays correctly
- [ ] No blank pages
- [ ] Responsive on mobile

### Features Work
- [ ] Can add players
- [ ] Can create tournaments
- [ ] Can score matches
- [ ] Leaderboard shows rankings
- [ ] Dashboard updates live

### Database Works
- [ ] Data appears in Firestore Console
- [ ] Data persists after refresh
- [ ] Multiple pages stay in sync
- [ ] No permission errors

### Performance
- [ ] App loads quickly
- [ ] Interactions are responsive
- [ ] No console errors
- [ ] Mobile is responsive

---

## Optimization Tasks (Optional)

- [ ] Enable Firestore caching
- [ ] Optimize bundle size
- [ ] Add proper error handling
- [ ] Set up error logging
- [ ] Enable CDN caching

---

## Security Tasks (Before Going Live)

- [ ] Review Firestore Rules
- [ ] Set up authentication (optional)
- [ ] Enable HTTPS (automatic)
- [ ] Update Rules for production
- [ ] Remove debug logging

---

## Maintenance Tasks (Ongoing)

- [ ] Monitor Firestore usage
- [ ] Check error logs weekly
- [ ] Backup data regularly
- [ ] Update dependencies monthly
- [ ] Monitor performance

---

## Launch Tasks

- [ ] Create landing page (optional)
- [ ] Write deployment blog post (optional)
- [ ] Share with friends/family
- [ ] Gather feedback
- [ ] Plan next features

---

## Final Verification

- [ ] App URL works
- [ ] All features functional
- [ ] Database syncing
- [ ] No errors in logs
- [ ] Performance acceptable

**Status:** ☐ Ready to Launch

---

## Troubleshooting Quick Links

| Problem | Solution |
|---------|----------|
| Build fails | Check ACTION_PLAN.md |
| Firebase error | See GITHUB_FIRESTORE_SETUP.md |
| Deployment issues | Check DEPLOYMENT.md |
| Environment error | Verify .env.local |
| Permission denied | Review Firestore Rules |

---

## Important URLs

- Firebase Console: https://console.firebase.google.com
- Vercel Dashboard: https://vercel.com/dashboard
- Your Repository: https://github.com/YOUR_USERNAME/badminton-tournament
- Documentation: ACTION_PLAN.md

---

## Contact & Support

Before contacting support, check:
1. GITHUB_FIRESTORE_SETUP.md
2. DEPLOYMENT.md
3. ACTION_PLAN.md
4. GITHUB_FIRESTORE_QUICK_REF.md

---

## Sign-Off

- [ ] All checks passed
- [ ] App is live
- [ ] Ready to use
- [ ] Ready to share

**Date Deployed:** _____________

**Live URL:** _____________

**Deployed By:** _____________

---

Congratulations! Your app is live! 🚀

Print this checklist and keep it handy during deployment.

