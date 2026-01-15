# 💬 Chat App

**Chat App** is a real‑time messaging application built with **Flutter** and **Firebase**, designed to provide fast, secure, and reliable one‑to‑one conversations across devices.  
It focuses on a production‑style experience with robust authentication, live message updates, and a clean, user‑friendly interface.

> Sign in, select a contact, and start chatting in real time — messages sync instantly between users with no manual refresh.

---

## ⚡ Core Features

- 🔐 **Secure authentication**
  - Email/password authentication using Firebase Authentication with proper error handling and validation.
  - Persistent sessions so users remain signed in until they explicitly log out.
  - Clear feedback for invalid credentials, connectivity issues, and edge cases.

- 💬 **Real‑time chat**
  - Bi‑directional, real‑time messaging powered by Firebase (Firestore or Realtime Database, based on configuration).
  - Each message includes sender, receiver/chat ID, and server timestamp to ensure correct ordering and consistency.
  - UI reacts to live streams/listeners, updating conversations instantly without pull‑to‑refresh.

- 👥 **Conversations & contacts**
  - Dedicated users/contacts screen to start or resume chats with any registered account.
  - Per‑conversation message history, with the option to show last message and time in the chat list for a messenger‑like feel.

- 📲 **Polished user experience**
  - Responsive UI built with Flutter widgets (lists, forms, input fields) optimized for mobile.
  - Typing area with send action, automatic scroll to the latest message, and basic loading/error states for network operations.
  - Structure ready to extend with features such as read receipts, typing indicators, or media messages.

---

## 🧱 Tech Stack

- **Framework:** Flutter  
- **Backend:** Firebase (Cloud Firestore or Realtime Database for storing users and messages)  
- **Authentication:** Firebase Authentication (`firebase_auth`) for user identity and session management  
- **Realtime Updates:** Streams / snapshot listeners from Firebase to keep chat views synchronized in real time  

---

## 🔐 Authentication Flow

The authentication flow is structured to mirror real‑world apps while staying simple to maintain and extend.

1. **App launch**
   - Firebase is initialized when the app starts.
   - The app checks for an existing authenticated Firebase user to decide the initial screen.

2. **Unauthenticated users**
   - Display a **Login / Register** screen.
   - Users can:
     - Create a new account with `createUserWithEmailAndPassword`.
     - Sign in using `signInWithEmailAndPassword`.

3. **Authenticated users**
   - Navigate directly to the main chat/home screen.
   - Show:
     - List of available users or conversations.
     - Optionally the last opened chat thread for quick resume.

4. **Session lifecycle**
   - On logout or auth state changes, the user is redirected back to the authentication screen.
   - All messages are associated with `FirebaseAuth.currentUser.uid` to link chats reliably to specific accounts.

---

## 🧵 Real‑Time Messaging Design

- Each message document/record typically contains:
  - `text`: message body.
  - `senderId`: UID of the sending user.
  - `receiverId` or `chatId`: to group messages into conversations.
  - `createdAt`: server timestamp for chronological ordering.
- The chat screen:
  - Subscribes to a messages collection/node filtered by conversation and ordered by `createdAt`.
  - Rebuilds automatically when new messages are added, edited, or removed, thanks to live snapshot streams.
- Sending a message:
  - On “Send”, the app writes a new message document/record to Firebase.
  - All connected clients listening to that conversation receive the update immediately and render the new message.

---

## 🚀 Getting Started

```bash
# Clone the repository
git clone https://github.com/your-username/chat_app.git
cd chat_app

# Install dependencies
flutter pub get

# Configure Firebase (Android / iOS)
# - Add google-services.json (Android)
# - Add GoogleService-Info.plist (iOS)
# - Initialize Firebase in main() as per official docs

# Run the app
flutter run
