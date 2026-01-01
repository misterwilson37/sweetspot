# The Sweet Spot - Firebase Edition

A game about finding the perfect spot for text placement on images.

## Quick Start (Firebase Already Configured!)

Your Firebase project (`ellisbell-c185c`) is already set up in `firebase-config.js`. You just need to:

### 1. Enable Firestore Database (if not already enabled)

1. Go to [Firebase Console](https://console.firebase.google.com/project/ellisbell-c185c)
2. Click "Firestore Database" in the left sidebar
3. If not already created, click "Create database"
4. Choose "Start in test mode" (or production mode if you prefer)
5. Click "Enable"

### 2. Run the Migration

1. Open `admin.html` in a browser
2. Go to the "Migration" tab
3. Click "Start Migration"
4. Wait for all 10 original images to upload

### 3. Play!

Open `game.html` and enjoy!

## Creating New Levels

1. Open `admin.html`
2. Upload an image
3. Select "Good Zone" or "Perfect Zone"
4. Choose text color (white/black)
5. Click and drag on the image to draw zones
6. Add hints and feedback as needed
7. Click "Save Level"

## File Structure

```
sweet-spot-game/
├── README.md           # This file
├── firebase-config.js  # Firebase configuration (pre-configured)
├── game.html           # The main game
└── admin.html          # Level editor/admin panel
```

## Data Storage

This app uses your existing `ellisbell-c185c` Firebase project with:
- **Firestore collection:** `levels` (stores level configurations)
- **Storage folder:** `game-images/` (stores uploaded images)

These are completely separate from your bell system data.

## Security (For Production)

If you want to restrict who can edit levels, update your Firestore rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /levels/{levelId} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

And Storage rules:
```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /game-images/{imageId} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```
