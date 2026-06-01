# Interlink 2026 — Evaluation Portal

A clean, modern, and responsive evaluation form for **Interlink 2026: A CSPC–UNAIR Cross-Campus Webinar**. This portal is styled to mirror the registration website's Slate design theme and runs entirely on client-side HTML/JS integrated with a secure, serverless Google Apps Script backend.

---

## 📂 Project Structure

```bash
├── index.html            # Main evaluation form layout and custom Slate CSS styles
├── app.js                # Frontend form validation, ratings check, and fetch submission logic
├── google-apps-script.js # Apps Script code (copy into Google Sheets container)
└── public/
    └── header.png        # Header banner image (mirrored from registration portal)
```

---

## ⚡ Setup & Deployment Guide

### 1. Assets Copying
Make sure to copy the header banner image `header.png` from the registration codebase directory to this project folder:
```bash
mkdir -p public
cp ../interlink_registration/public/header.png public/
```

### 2. Google Sheets & Apps Script Backend Setup
This project saves evaluations directly into a Google Sheet using Google Apps Script.

1. Create a new Google Sheet.
2. Go to **Extensions** > **Apps Script**.
3. Clear any default code in the editor and copy the contents of `google-apps-script.js` into the editor.
4. Click the **Save** (floppy disk) icon.

#### A. Authorization
Before deploying, authorize the script:
1. Select the `doPost` function from the dropdown next to "Debug" / "Run".
2. Click **Run**.
3. A popup will ask for permissions. Click **Review Permissions**, select your Google Account, click **Advanced**, click **Go to [Untitled project] (unsafe)**, and choose **Allow**.

#### B. Deployment
1. Click the **Deploy** button (top right) > **New deployment**.
2. Select **Web app** as the deployment type.
3. Configure the settings:
   - **Description**: `Interlink 2026 Evaluation Form Backend`
   - **Execute as**: `Me (your-email@gmail.com)`
   - **Who has access**: `Anyone` *(Crucial: Do not select "Only myself" or "Anyone with a Google Account")*
4. Click **Deploy**.
5. Copy the generated **Web App URL** (ends in `/exec`).

---

### 3. Link Frontend to Backend
Open `app.js` and paste your deployed Apps Script Web App URL into the `ENDPOINT_URL` constant on line 7:

```javascript
// Replace this URL with your deployed Google Apps Script Web App URL.
const ENDPOINT_URL = "https://script.google.com/macros/s/.../exec";
```

---

### 4. Hosting the Form
Host this folder on **Netlify**, **GitHub Pages**, or any static web hosting provider.

---

## 🛠️ Features

* **Slate Dark Accent Theme**: Visually coherent with the registration portal, utilizing Inter typography, custom radio layouts, and dynamic transition animations.
* **Inline Validation**:
  - Highlights unfilled rating criteria in red.
  - Ensures a valid email is inputted.
  - Requires explicit confirmation that the user's name is correct for certificate generation.
* **Redirect/CORS-Friendly Submission**: Submits payload using `text/plain` to avoid CORS preflight options blocking.
* **Google Apps Script Lock & Duplicate Protection**: Uses Apps Script's `LockService` to prevent simultaneous write conflicts and checks for existing emails to avoid duplicate evaluations.
