# Frost Notes - The Digital Winter

A modern, feature-rich note-taking application with a stunning winter-themed UI, multimedia support, and real-time synchronization.

## Features

### Core Functionality
- **Rich Text Notes** - Create, edit, and organize notes with titles and content
- **Real-time Sync** - Notes are automatically saved and synchronized across devices
- **Advanced Search** - Full-text search across titles, content, and tags
- **Tag System** - Organize notes with custom tags and filter by multiple tags
- **Responsive Design** - Works seamlessly on desktop, tablet, and mobile devices

### Multimedia Support
- **Drawing Canvas** - Create sketches and drawings directly in your notes
- **Photo Uploads** - Attach multiple images to your notes (up to 10MB per file)
- **Audio Recording** - Record and playback voice memos within notes
- **Media Management** - Preview, play, and remove multimedia attachments

### Advanced Features
- **Reminders** - Set date/time alerts for important notes
- **Theme Toggle** - Switch between dark winter theme and light spring theme
- **Keyboard Shortcuts** - Efficient navigation and note management
- **Real-time Notifications** - Visual feedback for all actions
- **Glassmorphism UI** - Modern, frosted glass aesthetic with smooth animations

## Technology Stack

- **Frontend**: Vanilla JavaScript (ES6+), HTML5, CSS3
- **Backend**: Firebase (Authentication, Firestore, Storage)
- **Animations**: GSAP (GreenSock Animation Platform)
- **Styling**: Custom CSS with CSS Variables and Flexbox/Grid
- **Icons**: Unicode emojis and custom styling

## Setup Instructions

### Prerequisites
- Modern web browser with JavaScript enabled
- Internet connection for Firebase services

### Firebase Configuration
1. Create a new Firebase project at [Firebase Console](https://console.firebase.google.com/)
2. Enable the following services:
   - **Authentication** (Email/Password provider)
   - **Firestore Database**
   - **Storage**
3. Get your Firebase configuration object
4. Replace the `firebaseConfig` object in the HTML file with your credentials:

```javascript
const firebaseConfig = {
    apiKey: "your-api-key",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "your-sender-id",
    appId: "your-app-id"
};
```

### Firestore Security Rules
Set up the following security rules in Firestore:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /notes/{noteId} {
      allow read, write: if request.auth != null && request.auth.uid == resource.data.userId;
      allow create: if request.auth != null && request.auth.uid == request.resource.data.userId;
    }
  }
}
```

### Storage Security Rules
Set up the following security rules for Firebase Storage:

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /photos/{userId}/{allPaths=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
    match /audio/{userId}/{allPaths=**} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

### Deployment
1. Save the HTML file as `index.html`
2. Deploy to any static hosting service:
   - **Firebase Hosting**: `firebase deploy`
   - **Netlify**: Drag and drop the HTML file
   - **Vercel**: Connect your GitHub repository
   - **GitHub Pages**: Push to a repository and enable Pages


## Screenshots
<img width="1895" height="848" alt="image" src="https://github.com/user-attachments/assets/b92d83fb-fefd-46af-8cd9-591e3779ebea" />
<img width="1896" height="852" alt="image" src="https://github.com/user-attachments/assets/7daea618-b0f9-49e8-80fc-eb9f5c10efe0" />
<img width="1897" height="846" alt="image" src="https://github.com/user-attachments/assets/4f24b01e-8644-4e60-82bd-995fa2594822" />
<img width="1898" height="849" alt="image" src="https://github.com/user-attachments/assets/6ea2878e-baff-48fd-ab31-2bf297d4668e" />
<img width="1895" height="844" alt="image" src="https://github.com/user-attachments/assets/b2946e02-5797-4b20-9c26-ee9676822942" />
<img width="1896" height="844" alt="image" src="https://github.com/user-attachments/assets/14833bae-7b62-4085-b213-555f2a236a15" />
<img width="1898" height="843" alt="image" src="https://github.com/user-attachments/assets/5e21e064-eee0-45bc-9462-a937bcbb4c0a" />
<img width="1904" height="850" alt="image" src="https://github.com/user-attachments/assets/2658a549-f777-4d24-854c-173d0657b99a" />
<img width="1899" height="844" alt="image" src="https://github.com/user-attachments/assets/48ee4c45-39eb-419e-b082-7f05f79b0c2f" />


## Usage Guide

### Getting Started
1. Open the application in your browser
2. Register a new account or sign in with existing credentials
3. Start creating notes with the intuitive interface

### Keyboard Shortcuts
- **Ctrl/Cmd + N**: Create new note
- **Ctrl/Cmd + S**: Save current note
- **Ctrl/Cmd + F**: Focus search bar
- **Escape**: Clear form and start fresh

### Creating Notes
1. Enter a title for your note
2. Add content in the text area
3. Optionally add multimedia:
   - Click "Draw" to open the drawing canvas
   - Use "Upload Images" to attach photos
   - Click "Record" to add voice memos
4. Set reminders if needed
5. Add tags for organization
6. Click "Save Entry" to store your note

### Drawing Features
- **Color Picker**: Choose drawing colors
- **Brush Size**: Adjust stroke width (1-20px)
- **Clear Canvas**: Reset the drawing
- **Hide/Show**: Toggle canvas visibility

### Audio Recording
- **Record**: Start recording audio (microphone permission required)
- **Stop**: End the recording session
- **Play**: Preview recorded audio
- **Delete**: Remove audio attachment

### Organizing Notes
- **Tags**: Add multiple tags to categorize notes
- **Search**: Use the search bar for full-text search
- **Filter**: Click tags in the filter section to show only related notes
- **Sort**: Notes are automatically sorted by creation date (newest first)

## Browser Compatibility

- **Chrome/Chromium**: Full support
- **Firefox**: Full support
- **Safari**: Full support (iOS 14.5+)
- **Edge**: Full support

### Required Permissions
- **Microphone**: For audio recording features
- **Storage**: For local file operations

## File Structure

```
frost-notes/
├── index.html          # Main application file
├── README.md          # Documentation

```

## Performance Notes

- **Images**: Automatically resized and compressed for optimal performance
- **Audio**: Recorded in WAV format for quality
- **Animations**: Hardware-accelerated CSS and GSAP animations
- **Caching**: Firebase automatically handles data caching
- **Offline**: Limited offline support through Firebase caching

## Security Features

- **Authentication**: Secure email/password authentication via Firebase
- **Data Isolation**: Users can only access their own notes
- **File Validation**: Client-side file type and size validation
- **XSS Protection**: All user content is properly escaped
- **HTTPS**: All Firebase communication uses HTTPS

## Known Limitations

- **File Size**: Individual files limited to 10MB
- **Browser Storage**: Drawing uses in-memory storage during editing
- **Mobile Drawing**: Touch drawing may have reduced precision on some devices

## Troubleshooting

### Common Issues
1. **Authentication Errors**: Verify Firebase configuration and enable Email/Password auth
2. **Upload Failures**: Check file size limits and internet connection
3. **Audio Not Working**: Ensure HTTPS and microphone permissions
4. **Notes Not Syncing**: Verify Firestore rules and user authentication

### Debug Mode
Open browser developer tools (F12) to view console logs and error messages.

## Contributing

This is a single-file application for simplicity. To contribute:

1. Fork the repository
2. Make your changes to the HTML file
3. Test thoroughly across browsers
4. Submit a pull request with detailed description

## License

This project is open source and available under the [MIT License](https://opensource.org/licenses/MIT).

## Support

For issues and questions:
- Check the browser console for error messages
- Verify Firebase configuration and security rules
- Ensure all required services are enabled in Firebase Console

---

**Frost Notes** - Where your thoughts crystallize in the digital winter. ❄️
