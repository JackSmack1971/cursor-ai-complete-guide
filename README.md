# **Cursor AI: Complete Guide**

### **Introduction**

Welcome to the **Cursor AI: Complete Guide**! In this guide, you’ll learn how to set up a **React** project integrated with **Firebase** and deploy it to **Firebase Hosting**, all while utilizing **GitHub** for version control.

By the end of this guide, you will:
- Have a functioning web application built with React.
- Use Firebase for hosting, real-time databases, and user authentication.
- Be able to version-control your project using GitHub and deploy it to Firebase for live hosting.

**Who is this guide for?**  
This guide is for beginners and intermediate developers who want to:
- Build a web app using React.
- Learn how to set up Firebase for hosting, databases, and authentication.
- Understand the process of deploying a project from local development to live hosting with GitHub and Firebase.

---

## **Table of Contents**

1. [Prerequisites](#prerequisites)
2. [Step 1: Create a New Project Directory](#step-1-create-a-new-project-directory)
3. [Step 2: Set Up Your Development Environment – Install Node.js and React](#step-2-set-up-your-development-environment--install-nodejs-and-react)
4. [Step 3: Connect Your Project to GitHub](#step-3-connect-your-project-to-github)
5. [Step 4: Launch Your React App Locally for Testing](#step-4-launch-your-react-app-locally-for-testing)
6. [Step 5: Set Up Firebase](#step-5-set-up-firebase)
7. [Step 6: Deploy to Firebase Hosting](#step-6-deploy-to-firebase-hosting)
8. [Step 7: Verify Firebase Hosting](#step-7-verify-firebase-hosting)
9. [Next Steps – Extending the Project](#next-steps-extending-the-project)
10. [Conclusion](#conclusion)

---
## **Setup Cursor AI Project:**

### **Prerequisites**

Before you begin, make sure you have the following installed:

- **Node.js** (version 14 or higher): This allows you to run JavaScript code on your machine and manage packages with npm. [Download Node.js](https://nodejs.org).
- **Git**: Git is a version control system that will allow you to manage changes in your project and push your code to GitHub. [Download Git](https://git-scm.com).
- **Firebase account**: Firebase is a platform that offers backend services like hosting, authentication, and databases. You’ll use Firebase Hosting to deploy your app. [Sign up for Firebase](https://firebase.google.com).

> **Why These Are Important:**  
> **Node.js** is required for running the React development environment. **Git** will allow you to version-control your project, and **Firebase** will handle hosting, databases, and authentication for your app.

---

## **Step 1: Create a New Project Directory**

1. **Create and navigate to your project folder**:
   - **Mac/Linux**:
     ```
     mkdir ~/YOURDIRECTORY
     cd ~/YOURDIRECTORY
     ```
   - **Windows**:
     ```
     mkdir %USERPROFILE%\YOURDIRECTORY
     cd %USERPROFILE%\YOURDIRECTORY
     ```

2. **Open the directory in your code editor**:
   ```bash
   code .
   ```

> **Note**: This creates a folder for your project files. Opening it in a code editor allows you to manage the project easily.

---

## **Step 2: Set Up Your Development Environment – Install Node.js and React**

### **Install Node.js**

- **Mac**: Install via Homebrew:
  ```
  brew install node
  ```

- **Linux**: Install via apt:
  ```
  sudo apt update && sudo apt install nodejs npm
  ```

- **Windows**: Download and install from [Node.js official website](https://nodejs.org).

> **Verify Node.js installation**:  
Run the following command to ensure Node.js is installed:
```
node -v
```

### **Initialize a React Project**

1. **Initialize a new React app**:
   ```
   npx create-react-app <YOUR_APP_NAME>
   cd <YOUR_APP_NAME>
   ```

> **Note**: Replace `<YOUR_APP_NAME>` with your desired app name. This command sets up the initial structure of your React app, allowing you to begin development immediately.

---

## **Step 3: Connect Your Project to GitHub**

### **Set Up Git and Push to GitHub**

#### **Step 1: Initialize Git and Add a README**

1. **Initialize Git in your project folder**:
   ```
   git init
   ```

2. **Create a README file and add some content**:
   ```
   echo "# <YOUR_REPO_NAME>" >> README.md
   ```

3. **Add the README file to Git**:
   ```
   git add README.md
   ```

4. **Commit your changes**:
   ```
   git commit -m "Initial commit"
   ```

5. **Set the default branch to `main`**:
   ```
   git branch -M main
   ```

#### **Step 2: Push Your Project to GitHub**

> **Generate and Use a Personal Access Token (PAT)**  
> Since GitHub has moved away from password-based authentication, you’ll need to create a Personal Access Token to push code to your repository. Follow these steps to create a PAT:
>
> 1. Navigate to **GitHub Settings -> Developer Settings -> Personal Access Tokens**.
> 2. Generate a new token and select the necessary scopes (`repo` for full control of repositories).
> 3. Copy the token (you won’t be able to see it again).
> 4. Use Git's credential helper to securely store your token:
>    ```
>    git config --global credential.helper cache
>    ```

1. **Add a remote repository using your PAT**:
   ```
   git remote add origin https://<YOUR_USERNAME>:<YOUR_PERSONAL_ACCESS_TOKEN>@github.com/<YOUR_USERNAME>/<YOUR_REPO_NAME>.git
   ```

2. **Push the code to GitHub**:
   ```
   git push -u origin main
   ```

---

## **Step 4: Launch Your React App Locally for Testing**

1. **Start the React development server**:
   ```
   npm start
   ```

2. **Open your browser** and navigate to [http://localhost:3000](http://localhost:3000). You should see the default React welcome screen.

> **Troubleshooting**:  
If port 3000 is already in use, React will prompt you to use a different port. You can free up the port by running:
```
npx kill-port 3000
```

---

## **Step 5: Set Up Firebase**

Firebase offers services like hosting, authentication, and Firestore (a NoSQL database) that integrate seamlessly with your React app.

### **Step 1: Install Firebase**

1. **Install Firebase in your React project**:
   ```
   npm install firebase
   ```

2. **Go to the Firebase Console** at [firebase.google.com](https://console.firebase.google.com) and log in.

3. **Create a new Firebase project**.

### **Step 2: Add Firebase to Your Web App**

1. In the Firebase Console, select **Web** as the platform.

2. Register your app and Firebase will provide you with a **configuration snippet**.

### **Step 3: Configure Firebase in Your Project**

1. **Create a `firebase.js` file** in the `src` directory:
   ```
   touch src/firebase.js
   ```

2. **Paste the Firebase configuration into `firebase.js`**:

   ```
   import { initializeApp } from 'firebase/app';
   import { getFirestore } from 'firebase/firestore';
   import { getAuth } from 'firebase/auth';

   // Firebase configuration, replace with your actual values
   const firebaseConfig = {
     apiKey: process.env.REACT_APP_FIREBASE_API_KEY,
     authDomain: process.env.REACT_APP_FIREBASE_AUTH_DOMAIN,
     projectId: process.env.REACT_APP_FIREBASE_PROJECT_ID,
     storageBucket: process.env.REACT_APP_FIREBASE_STORAGE_BUCKET,
     messagingSenderId: process.env.REACT_APP_FIREBASE_MESSAGING_SENDER_ID,
     appId: process.env.REACT_APP_FIREBASE_APP_ID
   };

   const app = initializeApp(firebaseConfig);
   const db = getFirestore(app);
   const auth = getAuth(app);

   export { db, auth };
   ```

> **What Are Environment Variables?**  
Environment variables are key-value pairs used to configure your app for different environments (local development, production). They help keep sensitive information, like API keys, safe and separate from your codebase. Firebase requires you to provide credentials for services like authentication and databases. By storing these values in environment variables, you avoid hardcoding sensitive data into your code.

> **Best Practice**: For security, store sensitive configuration data in environment variables using a `.env` file:
```
REACT_APP_FIREBASE_API_KEY="your-api-key"
REACT_APP_FIREBASE_AUTH_DOMAIN="your-auth-domain"
REACT_APP_FIREBASE_PROJECT_ID="your-project-id"
```

---

## **Step 6: Deploy to Firebase Hosting**

### **Step 1: Install Firebase CLI**

1

. **Install the Firebase CLI globally**:
   ```
   npm install -g firebase-tools
   ```

2. **Log in to Firebase**:
   ```
   firebase login
   ```

### **Step 2: Initialize Firebase in Your Project**

1. **Run the initialization command**:
   ```
   firebase init
   ```

2. **When prompted**:
   - Select **Hosting**.
   - Choose the Firebase project you created earlier.
   - Set the public directory to `build`.
   - Configure as a single-page app by typing `y`.
   - Do **not** overwrite `index.html`.

> **Explanation of Prompts**:
- **Hosting Setup**: Links your local app to Firebase Hosting.
- **Public Directory**: Use the `build` folder generated by React when you run `npm run build`. This contains the production-ready version of your app.
- **Single Page Application**: Select `y` so Firebase can handle routing properly for a React SPA.

### **Step 3: Build and Deploy Your App**

1. **Build your React app for production**:
   ```
   npm run build
   ```

2. **Deploy your app to Firebase**:
   ```
   firebase deploy
   ```

> **Common Issues During Deployment**:
1. **Build folder missing**: Ensure that you've run `npm run build` before deploying.
2. **Authentication Errors**: If you see authentication errors during deployment, confirm you're logged in by running:
   ```
   firebase login
   ```

---

## **Step 7: Verify Firebase Hosting**

After deploying, Firebase will provide a live URL for your app. Open this URL in your browser to verify that your app is live and functioning correctly.

---

## **Next Steps – Extending the Project**

### **Explore These Extensions**:

1. **Add Firebase Authentication**:
   - Integrate Firebase Authentication to allow users to sign in using Google, Facebook, or email/password.
   - Refer to [Firebase Authentication Docs](https://firebase.google.com/docs/auth).

2. **Use Firestore**:
   - Implement real-time database functionality with Firestore. Learn how to create, read, update, and delete documents in [Firestore Docs](https://firebase.google.com/docs/firestore).
   ```
   import { collection, addDoc } from 'firebase/firestore';

   async function addUser(db) {
     try {
       const docRef = await addDoc(collection(db, "users"), {
         name: "John Doe",
         email: "john.doe@example.com"
       });
       console.log("Document written with ID: ", docRef.id);
     } catch (e) {
       console.error("Error adding document: ", e);
     }
   }
   ```

3. **Set Up Continuous Deployment**:
   - Automate your deployments using **GitHub Actions** to deploy your app every time you push to your repository. Learn how to set up CI/CD with Firebase Hosting using [GitHub Actions](https://firebase.google.com/docs/hosting/github-integration).

---

## **Conclusion**

Congratulations on completing the **Cursor AI: Complete Guide**! You’ve learned how to:
- Set up a **React** project.
- Integrate it with **Firebase** for hosting and databases.
- Use **GitHub** for version control and deploying your app to **Firebase Hosting**.

By following this guide, you've deployed a live web application. Next, consider adding more features, such as **Firebase Authentication** or **Firestore**, and explore tools like **GitHub Actions** for continuous deployment. Happy coding!

---

### **Additional Resources**
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [Firebase Hosting Documentation](https://firebase.google.com/docs/hosting)
- [GitHub Actions for Firebase](https://firebase.google.com/docs/hosting/github-integration)

---
