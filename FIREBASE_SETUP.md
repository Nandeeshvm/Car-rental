# Firebase Setup Instructions

## 🔥 Fix Permission Error - Quick Solution

The "Missing or insufficient permissions" error occurs because Firebase Firestore rules are blocking access. Here are the steps to fix it:

## Option 1: Update Rules via Firebase Console (Recommended)

1. **Go to Firebase Console**: https://console.firebase.google.com/
2. **Select your project**: `car-rental-2037e`
3. **Navigate to Firestore Database**
4. **Click on "Rules" tab**
5. **Replace the existing rules with this code:**

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow read/write access for testing - TEMPORARY RULES
    match /{document=**} {
      allow read, write: if true;
    }
    
    // Customer Management Rules - Open access for testing
    match /customers/{customerId} {
      allow read, write: if true;
    }
  }
}
```

6. **Click "Publish" to deploy the rules**

## Option 2: Deploy via Firebase CLI

```bash
# 1. Login to Firebase
firebase login

# 2. Initialize the project
firebase use car-rental-2037e

# 3. Deploy the rules
firebase deploy --only firestore:rules
```

## Option 3: Test Firebase Connection First

1. **Go to your app**: http://localhost:3001
2. **Navigate to Customer Management**
3. **Click "🔧 Debug Firebase" tab**
4. **Click "Test Configuration"** - Should show all config values
5. **Click "Test Firebase Connection"** - This will show the exact error

## ⚠️ IMPORTANT SECURITY NOTE

The rules above allow **public access** for testing purposes. For production, you should implement proper authentication and more restrictive rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Production rules with authentication
    match /customers/{customerId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

## 🧪 After Fixing Rules

1. Go to Customer Management → Main interface
2. Try clicking "Add New Customer"
3. Fill in the form and submit
4. The error should be resolved!

## 📋 Your Current Firebase Config

- **Project ID**: car-rental-2037e
- **Auth Domain**: car-rental-2037e.firebaseapp.com
- **API Key**: Configured ✓
- **Storage Bucket**: Configured ✓

## 🔍 Troubleshooting

If you still get errors after updating rules:

1. **Wait 1-2 minutes** for rules to propagate
2. **Refresh your browser**
3. **Check Firebase Console** for any error messages
4. **Use the Debug Firebase tab** to test connection
5. **Check browser console** for detailed error messages

The most common issue is that Firebase rules need to be updated in the Firebase Console. The temporary rules above will allow your customer management system to work immediately.