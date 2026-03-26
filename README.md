# 🏸 Badminton Tournament Management System

A fully dynamic, real-time badminton tournament management web application built with **React 18**, **TypeScript**, and **Firestore**.

![React](https://img.shields.io/badge/react-18.3-blue)
![TypeScript](https://img.shields.io/badge/typescript-5.4-blue)
![Firebase](https://img.shields.io/badge/firebase-latest-orange)
![Vite](https://img.shields.io/badge/vite-5.2-green)

## ✨ Features

### 🎯 Core Features
- **Player Management** - Add, edit, delete players with ELO ratings
- **Tournament Management** - Create and manage round-robin tournaments
- **Match Scoring** - Record match scores and automatically calculate ELO ratings
- **Live Leaderboard** - Real-time player rankings
- **Dashboard** - Live statistics and tournament tracking
- **Real-Time Updates** - All data syncs instantly across pages

### 🔥 Technical Highlights
- ✅ **Cloud Database** - Firestore for scalable cloud storage
- ✅ **Real-Time Sync** - Automatic data synchronization
- ✅ **Type Safe** - Full TypeScript support
- ✅ **Modern UI** - Tailwind CSS for beautiful design
- ✅ **Fast Build** - Vite for lightning-fast development
- ✅ **Production Ready** - Optimized for deployment

## 🚀 Quick Start

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Firebase account

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/YOUR_USERNAME/badminton-tournament.git
cd badminton-tournament
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up Firebase**
   - Create a project at [Firebase Console](https://console.firebase.google.com)
   - Get your Firebase config
   - Create `.env.local` file:
   ```
   VITE_FIREBASE_API_KEY=YOUR_API_KEY
   VITE_FIREBASE_AUTH_DOMAIN=YOUR_PROJECT.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=YOUR_PROJECT_ID
   VITE_FIREBASE_STORAGE_BUCKET=YOUR_PROJECT.appspot.com
   VITE_FIREBASE_MESSAGING_SENDER_ID=YOUR_ID
   VITE_FIREBASE_APP_ID=YOUR_APP_ID
   ```

4. **Start development server**
```bash
npm run dev
```

5. **Open in browser**
   - Navigate to `http://localhost:5173`

For detailed setup instructions, see [GITHUB_FIRESTORE_SETUP.md](./GITHUB_FIRESTORE_SETUP.md)

## 📖 Documentation

| Document | Purpose |
|----------|---------|
| [GITHUB_FIRESTORE_SETUP.md](./GITHUB_FIRESTORE_SETUP.md) | 🚀 GitHub & Firestore setup guide |
| [QUICK_START.md](./QUICK_START.md) | 📚 Getting started with features |
| [IMPLEMENTATION_SUMMARY.md](./IMPLEMENTATION_SUMMARY.md) | 🔧 Technical details |
| [BEFORE_AND_AFTER.md](./BEFORE_AND_AFTER.md) | 📝 Code transformation |
| [INTERACTIVE_DEMO.md](./INTERACTIVE_DEMO.md) | 🎮 Demo tutorials |
| [VISUAL_GUIDE.md](./VISUAL_GUIDE.md) | 🎨 Visual diagrams |
| [MASTER_INDEX.md](./MASTER_INDEX.md) | 📚 Documentation index |

## 🏗️ Architecture

### Tech Stack
```
Frontend:
├── React 18
├── TypeScript
├── Tailwind CSS
└── Vite

Backend:
├── Firebase/Firestore
└── Cloud Functions (optional)

Database:
└── Firestore (Cloud)
```

### Data Structure
```
Firestore Collections:
├── players
│   ├── name
│   ├── email
│   ├── rating (ELO)
│   ├── wins
│   ├── losses
│   └── matchesPlayed
│
├── tournaments
│   ├── name
│   ├── date
│   ├── status
│   ├── playerIds
│   └── format
│
├── matches
│   ├── tournamentId
│   ├── player1Id
│   ├── player2Id
│   ├── scores
│   ├── winnerId
│   ├── status
│   └── round
│
└── standings
    ├── tournamentId
    ├── playerId
    ├── wins
    ├── losses
    └── pointDiff
```

## 🔄 Development Workflow

### Available Commands
```bash
# Development
npm run dev          # Start dev server with hot reload

# Production
npm run build        # Build for production
npm run preview      # Preview production build locally

# Firebase
firebase deploy      # Deploy to Firebase Hosting
firebase serve       # Test Firebase locally
```

### Project Structure
```
src/
├── App.tsx               # Main router
├── main.tsx             # Entry point
├── components/
│   └── Layout.tsx       # Navigation layout
├── pages/
│   ├── Dashboard.tsx    # Main dashboard
│   ├── Players.tsx      # Player management
│   ├── Tournaments.tsx  # Tournament management
│   ├── Leaderboard.tsx  # Rankings
│   └── TournamentDetail.tsx  # Match scoring
├── lib/
│   ├── db-firestore.ts  # Firestore database
│   ├── elo.ts          # ELO rating system
│   └── roundRobin.ts   # Tournament logic
└── styles/
    └── index.css        # Global styles
```

## 🌐 Deployment

### Firebase Hosting
```bash
npm run build
firebase deploy
```

### GitHub Pages
See [GITHUB_FIRESTORE_SETUP.md](./GITHUB_FIRESTORE_SETUP.md) for detailed instructions

### Vercel
```bash
npm run build
vercel
```

## 📊 Key Features Explained

### Real-Time Leaderboard
- Player rankings update instantly as matches are scored
- ELO ratings calculated and applied in real-time
- Tier assignments update automatically

### Live Tournament Tracking
- Progress bar updates as matches complete
- Standings recalculate automatically
- Tournament status updates in real-time

### Player Management
- Add/edit/delete players with instant sync
- Rating changes reflected across all pages
- Win/loss records updated automatically

### ELO Rating System
- Automatic calculation based on match results
- Accounts for skill differences
- Tier-based classification

## 🔐 Security

**For Development:**
Firestore Rules are set to allow all read/write operations.

**For Production:**
1. Enable Firebase Authentication
2. Update Firestore Rules to require authentication
3. Implement proper access control
4. Use environment variables for secrets

## 📝 Environment Variables

Create `.env.local` (never commit this file):
```
VITE_FIREBASE_API_KEY=...
VITE_FIREBASE_AUTH_DOMAIN=...
VITE_FIREBASE_PROJECT_ID=...
VITE_FIREBASE_STORAGE_BUCKET=...
VITE_FIREBASE_MESSAGING_SENDER_ID=...
VITE_FIREBASE_APP_ID=...
```

See `.env.example` for template.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📋 Roadmap

- [ ] User authentication
- [ ] Photo uploads for players
- [ ] Tournament bracket view
- [ ] Match statistics and analytics
- [ ] Mobile app version
- [ ] Real-time notifications
- [ ] Team tournaments
- [ ] Export tournament results

## 🐛 Troubleshooting

### Firebase Config Not Found
```
Solution: Create .env.local with correct Firebase credentials
```

### Firestore Permission Denied
```
Solution: Check Firestore Rules allow read/write
```

### Data Not Syncing
```
Solution: Check browser console for errors and Firebase config
```

See [GITHUB_FIRESTORE_SETUP.md](./GITHUB_FIRESTORE_SETUP.md) for more troubleshooting.

## 📄 License

MIT License - see LICENSE file for details

## 👥 Support

- 📖 Read the [documentation](./MASTER_INDEX.md)
- 🔍 Check [FAQ](#faq)
- 💬 Open an issue on GitHub

## FAQ

**Q: Can I use this without Firebase?**
A: The app is optimized for Firestore. For local development, you can modify db-firestore.ts to use IndexedDB.

**Q: How do I add custom tournament formats?**
A: See `src/lib/roundRobin.ts` and modify the tournament generation logic.

**Q: Can I deploy to my own server?**
A: Yes, build with `npm run build` and serve the `dist` folder. You'll need a backend for Firestore rules or use Firebase Hosting.

**Q: How do I customize the ELO rating formula?**
A: Edit `src/lib/elo.ts` and modify the `calculateNewRatings` function.

## 🎉 Credits

Built with ❤️ using React, TypeScript, Firebase, and Tailwind CSS

---

**Live Demo:** [Firebase Hosting URL - after deployment]

**Repository:** https://github.com/YOUR_USERNAME/badminton-tournament

**Issues & Feedback:** https://github.com/YOUR_USERNAME/badminton-tournament/issues

---

Last Updated: March 26, 2026
Version: 2.0 (Firestore Edition)

