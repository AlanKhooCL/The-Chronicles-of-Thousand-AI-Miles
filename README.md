# 🌌 Journeys & Ledgers: Beyond Journey's End

A beautifully crafted, entirely serverless web application that serves as your ultimate travel companion. Inspired by the ethereal aesthetic of *Frieren: Beyond Journey's End*, this app combines an **AI-Powered Trip Planner** and an **Intelligent Group Expense Splitter** into a single, seamless, mobile-optimized experience.

Built entirely within a single HTML file, this application leverages **Firebase Firestore** for scalable data storage and the **Firebase Vertex AI SDK** for secure, client-side generative AI. No Node.js, Webpack, or traditional backend required.

---

## ✨ Key Features

### 🗺️ The Planner's Grimoire (AI Trip Planner)
* **Generative AI Itineraries:** Instantly generate highly detailed, realistic travel itineraries based on simple text prompts. Choose your magic engine (Gemini 2.5 Flash, 2.5 Pro, or 3.0 Flash).
* **Interactive Dark-Mode Maps:** Integrated Leaflet.js maps dynamically plot your daily activities, showing numbered pins and dotted routes, perfectly styled to match the dark UI.
* **AI Editor:** Don't like a specific day? Use the AI Chat Modal to instantly rewrite specific parts of your itinerary (e.g., "Swap day 2 lunch for sushi").
* **Live Budget Tracking:** Track your base estimates and actual daily spending in real-time.

### ⚖️ The Debt Ledger (Group Expense Splitter)
* **Tabbed Navigation:** Effortlessly switch between Overview, Party Management, Expense Ledger, and Settlement screens.
* **Smart Settlement Algorithm:** Automatically calculates the most efficient way to settle group debts, minimizing the number of transactions needed.
* **Vibrating Debt Chart:** A dynamic Chart.js line graph tracks total group debt over time. If unsettled capital spikes, the chart physically starts vibrating on screen!
* **Categorized Spending:** Automatically breaks down your group's spending by category and by person using visual progress bars.
* **Export for Chat:** One-click copy formats your settlements into a clean text block perfect for WhatsApp or Telegram.

### 🎨 The Aesthetic & UX
* **Mystical UI:** Frosted glass panels, enchanted iron signposts, glowing runes, and elegant typography (`Cinzel` and `Crimson Pro`).
* **Particle Physics:** Custom HTML5 Canvas animations featuring falling magical petals and floating mana orbs that pause when you enter the app to save battery.
* **Deep Linking:** Easily share a specific trip or ledger with friends via URL parameters (e.g., `?planner=TripID` or `?ledger=LedgerID`).

---

## 📈 The Journey: Features Progression

This application didn't start as a masterpiece; it evolved through several major architectural iterations:

* **v1.0 - The Static Seed:** Started as a beautifully styled but static HTML/Tailwind template with hardcoded JSON data, basic cherry blossom animations, and a standard Leaflet map.
* **v2.0 - The AI Awakening:** Integrated the Gemini API directly into the frontend. The app could now dynamically generate full JSON itineraries based on user prompts.
* **v3.0 - The GAS Backend:** Moved API calls and storage to a Google Apps Script (GAS) backend. This secured the API key, bypassed CORS issues, and allowed trips to be saved permanently to the cloud.
* **v4.0 - The Great Merge:** A separate "Who pay Who?" expense-splitting app was successfully integrated into the ecosystem. The UI was updated to allow users to choose between the Planner and the Ledger.
* **v5.0 - The Frieren Overhaul:** Completely redesigned the UI to match a dark, mystical fantasy aesthetic. Replaced standard navigation with interactive crossroads signposts, converted maps to dark mode, and added deep-linking for seamless sharing.
* **v6.0 - The Firebase Ascension (Current):** Deprecated Google Apps Script in favor of **Firebase Firestore** to support scalable storage and concurrent ledger editing. Implemented the **Firebase Vertex AI SDK**, allowing the app to securely prompt Gemini directly from the client without exposing API keys, protected by Firebase Anonymous Authentication.

---

## 🛠️ Tech Stack

* **Frontend:** HTML5, Vanilla JavaScript, Tailwind CSS (via CDN)
* **Icons & Fonts:** Lucide Icons, Google Fonts (Cinzel, Crimson Pro, DM Sans)
* **Mapping & Charts:** Leaflet.js, Chart.js
* **Backend / Database:** Firebase Firestore (NoSQL)
* **Authentication:** Firebase Auth (Anonymous Sign-In for security rules)
* **AI Engine:** Firebase Vertex AI SDK (Gemini 2.0/2.5/3.0 models)

---

## 🚀 Setup & Installation

To run this application yourself, you need to configure a Firebase project.

### Step 1: Set up Firebase
1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. Enable **Firestore Database** (Start in production mode).
3. Enable **Authentication** and turn on the **Anonymous** sign-in provider.
4. Go to **Build > Vertex AI in Firebase** and enable the API for your project.

### Step 2: Configure Firestore Security Rules
Go to the **Rules** tab in your Firestore Database and paste the following to allow authenticated (anonymous) users to read and write:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /planner_trips/{document=**} {
      allow read, write: if request.auth != null;
    }
    match /debt_ledgers/{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
