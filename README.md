# BookSwap App 📚

A simple book trading app where people can swap books with each other. Built with Flutter and Firebase.

## What does this app do?

BookSwap lets you:
- **List books** you want to trade away
- **Browse books** other people are offering
- **Request swaps** with other users
- **Chat** with people about book trades
- **Get notifications** when someone wants your books

## Screenshots
![Page 1](<android/Assets/Screenshot 2025-11-09 111416.png>)
![Page 2](<android/Assets/Screenshot 2025-11-09 111440.png>)
![Page 3](<android/Assets/Screenshot 2025-11-09 111449.png>)
![Page 4](<android/Assets/Screenshot 2025-11-09 111504.png>)

### Need this application

### Step 1: Get the code

```bash
git clone <git@github.com:Kelvin364/Book-swap-App.git>
cd bookswap_app
```

### Step 2: Install Flutter packages

```bash
flutter pub get
```

### Step 3: Set up Firebase

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create a new project called "BookSwap"
3. Add an Android app (and iOS if needed)
4. Download the config files:
   - `google-services.json` → put in `android/app/`
   - `GoogleService-Info.plist` → put in `ios/Runner/` (if using iOS)

### Step 4: Enable Firebase services

In your Firebase project, turn on:
- **Authentication** (Email/Password)
- **Firestore Database** 
- **Storage** (for book photos)
- **Cloud Messaging** (for notifications)

### Step 5: Set up Firestore rules

Go to Firestore → Rules and paste this:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users can read/write their own data
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    
    // Anyone can read books, only owners can write
    match /books/{bookId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == resource.data.ownerId;
    }
    
    // Chat messages - only participants can access
    match /chats/{chatId} {
      allow read, write: if request.auth != null && 
        request.auth.uid in resource.data.participants;
    }
  }
}
```

### Step 6: Run the app

```bash
flutter run
```

## Technologies used

- **Flutter** - Mobile app framework
- **Firebase Auth** - User login/signup
- **Firestore** - Database for books and chats
- **Firebase Storage** - Store book photos
- **Provider** - State management
- **Cloud Messaging** - Push notifications



## Contributing

Want to help improve BookSwap?

1. Fork this repository
2. Create a new branch: `git checkout -b my-feature`
3. Make your changes
4. Test everything works
5. Submit a pull request

## Need help?

- Check [Flutter documentation](https://flutter.dev/docs)
- Look at [Firebase guides](https://firebase.google.com/docs)
- Create an issue in this repository

## License

This project is open source. Feel free to use and modify it.

