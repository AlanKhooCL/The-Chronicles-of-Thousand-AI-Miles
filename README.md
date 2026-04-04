# 🌌 Journeys & Ledgers: Beyond Journey's End

A beautifully crafted, entirely serverless web application that serves as your ultimate travel companion. This app combines an **AI-Powered Trip Planner** and an **Intelligent Group Expense Splitter** into a single, seamless, mobile-optimized experience.

Built entirely within a single HTML file, this application leverages **Firebase Firestore** for scalable data storage and the **Firebase Vertex AI SDK** for secure, client-side generative AI. No Node.js, Webpack, or traditional backend required.

---

## ✨ Key Features

### 🗺️ The Planner's Grimoire (AI Trip Planner)
* **Generative AI Itineraries:** Instantly generate highly detailed, realistic travel itineraries based on simple text prompts.
* **Auto-Generating Map Routes:** Simply type a location name in edit mode, and the app automatically geocodes the coordinates (via OpenStreetMap) to plot numbered markers and dashed daily routes on an interactive Leaflet map.
* **Smart URL Detection:** Drop a link into an activity description, and the app will automatically convert the activity title into a clickable hyperlink while keeping your description text clean.
* **Live Budget Tracking:** Track your base estimates and actual daily spending in real-time, with visual progress bars.
* **Rich Inline Editing:** Seamlessly edit titles, dates (via native date pickers), descriptions, and costs directly on the page without navigating away.

### ⚖️ The Debt Ledger (Group Expense Splitter)
* **Interactive Cross-Filtering:** Click on any person's name in the "Who spent what?" overview to instantly filter the category chart, visualizing exactly what that specific individual spent their money on.
* **Smart Settlement Algorithm:** Automatically calculates the most efficient way to settle group debts, providing explicit ("A needs to pay B") instructions to minimize the number of transactions needed.
* **Timestamped History:** Every expense is logged with exact creation timestamps for complete transparency. 
* **Vibrating Debt Chart:** A dynamic Chart.js line graph tracks total group debt over time. If unsettled capital spikes, the chart physically starts vibrating on screen!
* **Export for Chat:** One-click copy formats your settlements into a clean text block perfect for WhatsApp or Telegram.

### 🎨 The Aesthetic & UX
* **Mobile-First Design:** Fully responsive flex and grid layouts ensure that side-by-side content gracefully stacks and remains readable on mobile devices.
* **Immersive UI:** A light, watercolor aesthetic with grain textures, clean serif/sans-serif typography (`Newsreader` and `Plus Jakarta Sans`), and elegant loading animations.
* **Deep Linking:** Easily share a specific trip or ledger with friends via URL parameters (e.g., `?planner=TripID` or `?ledger=LedgerID`).

---

## 📈 The Journey: Features Progression

This application didn't start as a masterpiece; it evolved through several major architectural iterations:

* **v1.0 - The Static Seed:** Started as a beautifully styled but static HTML/Tailwind template with hardcoded JSON data and a standard Leaflet map.
* **v2.0 - The AI Awakening:** Integrated the Gemini API directly into the frontend. The app could now dynamically generate full JSON itineraries based on user prompts.
* **v3.0 - The GAS Backend:** Moved API calls and storage to a Google Apps Script (GAS) backend. This secured the API key, bypassed CORS issues, and allowed trips to be saved permanently to the cloud.
* **v4.0 - The Great Merge:** A separate "Who pay Who?" expense-splitting app was successfully integrated into the ecosystem. The UI was updated to allow users to choose between the Planner and the Ledger from a central crossroads.
* **v5.0 - The UI Overhaul:** Completely redesigned the UI to match a highly stylized aesthetic. Replaced standard navigation with interactive signposts, added custom icons, and implemented deep-linking for seamless sharing.
* **v6.0 - The Firebase Ascension:** Deprecated Google Apps Script in favor of **Firebase Firestore** to support scalable storage and concurrent ledger editing. Implemented the **Firebase Vertex AI SDK**, allowing the app to securely prompt Gemini directly from the client without exposing API keys, protected by Firebase Anonymous Authentication.
* **v7.0 - The Interactive Polish (Current):** A massive quality-of-life and automation update. Implemented auto-geocoding for locations to dynamically generate map routes, smart URL detection in itineraries, native date pickers, and comprehensive mobile layout fixes. Upgraded the Ledger with timestamped logs, explicit settlement instructions, and an interactive cross-filtering system to view individual category spending.

---

## 🛠️ Tech Stack

* **Frontend:** HTML5, Vanilla JavaScript, Tailwind CSS (via CDN)
* **Icons & Fonts:** Lucide Icons, Google Fonts (Newsreader, Plus Jakarta Sans)
* **Mapping & Charts:** Leaflet.js, Chart.js, OpenStreetMap (Nominatim API)
* **Backend / Database:** Firebase Firestore (NoSQL)
* **Authentication:** Firebase Auth (Anonymous Sign-In for security rules)
* **AI Engine:** Firebase Vertex AI SDK (Gemini models)

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
