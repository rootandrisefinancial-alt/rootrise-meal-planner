# Root & Rise Meal Planner — Deployment Guide
### How to turn your app into a live, installable web app (PWA)

---

## What you're building

By the end of this guide you will have:
- A live URL (e.g. `mealplanner.rootandrisefinancial.ca`) that clients can visit
- An app that installs to a phone's home screen like a real app
- Client data that saves automatically between sessions
- Free hosting, forever

**Time required:** 1–2 hours, no coding required.

**Tools you'll use (all free):**
- GitHub — stores your app files online
- Vercel — hosts and publishes your app live
- Your domain registrar (or Squarespace) — connects your custom domain

---

## Part 1 — Set up GitHub (10 minutes)

GitHub is where your app files live. Think of it like a Google Drive, but for code.

**Step 1.1 — Create a free GitHub account**
1. Go to github.com
2. Click "Sign up" and create a free account
3. Verify your email

**Step 1.2 — Create a new repository**
1. Once logged in, click the green "New" button (top left)
2. Name it: `rootrise-meal-planner`
3. Make sure it's set to **Public**
4. Check "Add a README file"
5. Click "Create repository"

**Step 1.3 — Upload your app files**

You need three files total. Start with the React app file I built for you (`rootrise-meal-planner.jsx`), then create the two additional files below.

In your new repository, click "Add file" → "Create new file"

---

**File 1 of 3 — `package.json`**

Name the file `package.json` and paste this exactly:

```json
{
  "name": "rootrise-meal-planner",
  "version": "1.0.0",
  "private": true,
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  },
  "scripts": {
    "start": "react-scripts start",
    "build": "react-scripts build"
  },
  "browserslist": {
    "production": [">0.2%", "not dead", "not op_mini all"],
    "development": ["last 1 chrome version"]
  }
}
```

Click "Commit changes" (green button, bottom of page).

---

**File 2 of 3 — `public/index.html`**

Click "Add file" → "Create new file"
Name it `public/index.html` and paste this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#3D4A2E" />
    <meta name="description" content="Root & Rise Meal Planner — a budgeting tool for everyday Canadians" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>Root & Rise Meal Planner</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

Click "Commit changes."

---

**File 3 of 3 — `public/manifest.json`**

Click "Add file" → "Create new file"
Name it `public/manifest.json` and paste this:

```json
{
  "short_name": "Meal Planner",
  "name": "Root & Rise Meal Planner",
  "icons": [
    {
      "src": "favicon.ico",
      "sizes": "64x64 32x32 24x24 16x16",
      "type": "image/x-icon"
    }
  ],
  "start_url": ".",
  "display": "standalone",
  "theme_color": "#3D4A2E",
  "background_color": "#F5F0E8"
}
```

Click "Commit changes."

---

**Upload the app file**

1. Click "Add file" → "Upload files"
2. Create a folder called `src` — you do this by typing `src/` before the filename
3. Upload `rootrise-meal-planner.jsx` and rename it to `src/App.jsx`
4. Also create a new file at `src/index.js` with this content:

```javascript
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<React.StrictMode><App /></React.StrictMode>);
```

Click "Commit changes."

---

## Part 2 — Deploy with Vercel (10 minutes)

Vercel takes your GitHub files and publishes them live. It's free and automatic — every time you update a file in GitHub, the live app updates itself.

**Step 2.1 — Create a Vercel account**
1. Go to vercel.com
2. Click "Sign Up" → choose "Continue with GitHub"
3. Authorize Vercel to access your GitHub

**Step 2.2 — Import your project**
1. On your Vercel dashboard, click "Add New" → "Project"
2. Find `rootrise-meal-planner` in the list and click "Import"
3. Under "Framework Preset" select **Create React App**
4. Leave everything else as default
5. Click "Deploy"

Vercel will build and deploy your app — this takes about 60–90 seconds.

**Step 2.3 — Get your live URL**

Once deployed, Vercel gives you a URL that looks like:
`rootrise-meal-planner.vercel.app`

Your app is now live! Test it in your browser and on your phone.

---

## Part 3 — Connect your custom domain (15 minutes)

This step gives you a branded URL like `mealplanner.rootandrisefinancial.ca` instead of the Vercel URL. Skip this for now if you want to test first.

**Step 3.1 — Add domain in Vercel**
1. In Vercel, go to your project → "Settings" → "Domains"
2. Type `mealplanner.rootandrisefinancial.ca` and click "Add"
3. Vercel will show you a CNAME record to copy — it looks like:
   - Name: `mealplanner`
   - Value: `cname.vercel-dns.com`

**Step 3.2 — Add the CNAME in your domain settings**

If your domain is managed through Squarespace:
1. Go to your Squarespace account → Domains → rootandrisefinancial.ca → DNS Settings
2. Click "Add Record" → choose "CNAME"
3. Paste in the Name and Value from Vercel
4. Save

DNS changes take 10 minutes to a few hours to go live. Once it's active, your branded URL will work.

---

## Part 4 — Make it installable on phones (5 minutes)

The `manifest.json` file you created in Part 1 already makes this a Progressive Web App (PWA). Here's how clients install it:

**On iPhone (Safari):**
1. Open the app URL in Safari
2. Tap the Share button (box with arrow)
3. Scroll down and tap "Add to Home Screen"
4. Tap "Add" — done

**On Android (Chrome):**
1. Open the app URL in Chrome
2. Chrome will show a banner that says "Add to Home Screen" automatically
3. Or tap the three-dot menu → "Add to Home Screen"

The app will appear on their home screen with its own icon, just like a downloaded app. It works offline too.

---

## Part 5 — Share with clients

Once live, here's how to deliver it:

**As a bonus with Custom Budget package:**
Include the URL in your client onboarding email or welcome document. Example line:

> "As a Custom Budget client, you also get access to the Root & Rise Meal Planner — a free tool to track your kitchen inventory, plan your weekly meals, and generate your grocery list automatically. Visit [your URL] and add it to your phone's home screen for easy access."

**As a standalone paid resource ($10–$25):**
Use a tool like Gumroad or Stan Store to sell access. Set up a simple product page, and after purchase the client receives the URL. No account system needed — the URL is the product.

---

## Troubleshooting

**"Page not found" after uploading files**
Make sure your files are in the right folders: `src/App.jsx`, `src/index.js`, `public/index.html`, `public/manifest.json`, `package.json` (root level).

**App looks broken or won't load**
Go to Vercel → your project → "Deployments" tab → click the latest deployment → "View Build Logs" to see what went wrong. Screenshot the error and send it to a developer or share with Claude.

**Domain isn't connecting**
DNS changes can take up to 24 hours. Check back the next day. If it's still not working, double-check the CNAME record values match exactly what Vercel provided.

**Client data not saving**
The app uses the browser's local storage. Data saves per device and per browser. If a client clears their browser data or switches devices, their data will reset. This is a known limitation — a future upgrade would add cloud accounts to sync across devices.

---

## Summary checklist

- [ ] GitHub account created
- [ ] Repository created: `rootrise-meal-planner`
- [ ] `package.json` added (root)
- [ ] `public/index.html` added
- [ ] `public/manifest.json` added
- [ ] `src/App.jsx` uploaded (your meal planner file)
- [ ] `src/index.js` added
- [ ] Vercel account created and linked to GitHub
- [ ] Project imported and deployed in Vercel
- [ ] Live URL tested in browser and on phone
- [ ] Custom domain connected (optional)
- [ ] App added to home screen (test the install flow yourself first!)

---

*Built for Root & Rise Financial Coaching | rootandrisefinancial.ca*
