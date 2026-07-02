# Flutter Chat App 💬

A real-time group chat application built with Flutter and Firebase. Users can create accounts, upload profile pictures, and participate in live group conversations.

## Features ✨

- **User Authentication**
  - Email and password registration
  - Secure login system
  - User profile with custom username
  - Profile picture upload

- **Real-time Messaging**
  - Send and receive messages instantly
  - Group chat functionality
  - Message history persistence
  - Real-time message synchronization

- **User Experience**
  - Clean and intuitive UI
  - Loading indicators during authentication
  - Form validation for inputs
  - Error handling with user-friendly messages

## Screenshots 📱

_Add your app screenshots here_

## Technologies Used 🛠️

- **Flutter** - Cross-platform mobile development framework
- **Firebase Authentication** - User authentication and management
- **Cloud Firestore** - Real-time NoSQL database for messages
- **Firebase Storage** - Profile picture storage
- **Dart** - Programming language

## Prerequisites 📋

Before running this project, make sure you have:

- Flutter SDK (latest stable version)
- Dart SDK
- Android Studio / VS Code with Flutter extensions
- Firebase account
- Android/iOS device or emulator

## Installation 🚀

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd chatting_app
```

### 2. Install dependencies

```bash
flutter pub get
```

### 3. Firebase Setup

1. Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)

2. Enable the following Firebase services:
   - **Authentication** (Email/Password provider)
   - **Cloud Firestore**
   - **Firebase Storage**

3. Download and add Firebase configuration files:

   **For Android:**
   - Download `google-services.json` from Firebase Console
   - Place it in `android/app/` directory

   **For iOS:**
   - Download `GoogleService-Info.plist` from Firebase Console
   - Place it in `ios/Runner/` directory

4. Configure FlutterFire:

```bash
# Install FlutterFire CLI
dart pub global activate flutterfire_cli

# Configure Firebase for your Flutter project
flutterfire configure
```

### 4. Firestore Security Rules

Set up the following security rules in Firebase Console:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
    
    match /messages/{messageId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
    }
  }
}
```

### 5. Firebase Storage Rules

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /user_image/{userId}/{fileName} {
      allow read: if request.auth != null;
      allow write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### 6. Run the app

```bash
flutter run
```

## Project Structure 📁

```
lib/
├── main.dart                      # App entry point
├── screens/
│   ├── auth.dart                  # Authentication screen (login/signup)
│   ├── chat.dart                  # Main chat screen
│   └── splash.dart                # Splash screen
└── widgets/
    ├── chat_message.dart          # Message list widget
    ├── new_message.dart           # Message input widget
    └── user_image_picker.dart     # Profile picture picker

android/
└── app/
    └── google-services.json       # Firebase config for Android

ios/
└── Runner/
    └── GoogleService-Info.plist   # Firebase config for iOS
```

## Firestore Data Structure 🗄️

### Users Collection

```javascript
users/{userId}
├── email: string
├── UserName: string
└── image_url: string (optional)
```

### Messages Collection

```javascript
messages/{messageId}
├── text: string
├── createAt: timestamp
├── userId: string
└── userName: string
```

## Usage 📖

1. **Sign Up**
   - Open the app
   - Click "Sign Up"
   - Upload a profile picture
   - Enter username, email, and password
   - Click "SignUp" button

2. **Login**
   - Enter your registered email and password
   - Click "Login" button

3. **Send Messages**
   - Type your message in the text field
   - Press the send button
   - Messages appear in real-time for all users

4. **Logout**
   - Click the logout icon in the app bar

## Configuration ⚙️

### Minimum Password Length
Located in `lib/screens/auth.dart`:
```dart
validator: (value) {
  if (value == null || value.isEmpty || value.length < 6) {
    return 'Password must be at least 6 characters long.';
  }
  return null;
}
```

### Username Requirements
Located in `lib/screens/auth.dart`:
```dart
validator: (value) {
  if (value == null || value.isEmpty || value.trim().length < 4) {
    return 'Please enter a Valid username.';
  }
  return null;
}
```

## Known Issues & Fixes 🐛

- Ensure all Firebase services are enabled in Firebase Console
- Check that Firebase configuration files are correctly placed
- Verify internet connection for real-time sync
- Make sure Firebase Storage rules allow authenticated uploads

## Future Enhancements 🚀

- [ ] Private one-on-one messaging
- [ ] User online/offline status
- [ ] Message read receipts
- [ ] Typing indicators
- [ ] Push notifications
- [ ] Image and file sharing in chat
- [ ] Message reactions and replies
- [ ] User search functionality
- [ ] Block/report users
- [ ] Message deletion
- [ ] Dark mode support

## Contributing 🤝

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the project
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License 📄

This project is open source and available under the [MIT License](LICENSE).

## Author ✍️

Created by [Your Name]

## Acknowledgments 🙏

- Flutter team for the amazing framework
- Firebase for backend services
- Flutter community for helpful resources

## Support 💬

For support, email [your-email@example.com] or create an issue in the repository.

---

**Happy Chatting! 🎉**
