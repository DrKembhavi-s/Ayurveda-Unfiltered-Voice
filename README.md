# 🌿 Dr. Kembhavi's Ayurveda Unfiltered Voice

> *A confidential, Firebase-secured platform for reform voices in Ayurveda education — Academic, Clinical, Research, Administrative, and Development.*

**Live Platform:** (https://DrKembhavi-s.github.io/ayurveda-unfiltered-voice)  
**Blog:** [drkembhavi-s.github.io](https://drkembhavi-s.github.io)  
**Developed by:** Dr. Aakash Kembhavi, MD Ayurveda | MS Counselling & Psychotherapy

---

## 📋 Overview

Dr. Kembhavi's Ayurveda Unfiltered Voice is a single-file web platform built with HTML, CSS, and JavaScript, backed by Google Firebase Firestore. It provides a safe, structured, and confidential space for Ayurveda students, PG scholars, faculty, and professionals to share honest feedback, discuss reforms, register institutions, generate reform proposals, and participate in community polls.

The platform is hosted on GitHub Pages and requires no server, no backend framework, and no paid infrastructure beyond a free Firebase project.

---

## ✨ Features

### 🎓 For UG Students (BAMS)
- Anonymous private feedback on curriculum, teaching, practical training, and ethical concerns
- Subject-specific feedback with full BAMS subject dropdown
- Star rating system
- What helped / What hindered structured fields
- Public Idea Board — post, read, and upvote reform ideas
- Admin-created polls with anonymous voting

### 📚 For PG Scholars
- All UG student features
- Optional confidential PG section covering:
  - Synopsis writing experience
  - Guide-scholar relationship
  - Research infrastructure quality
  - Conference and publication support
  - Open comments for ethical concerns and authorship issues

### 👨‍🏫 For Faculty & Professionals
- Discussion Forum for Academic, Clinical, Research, Administrative, and Development reforms
- Anonymous or named posting with reaction system (Support / Helpful / Concerned)
- Community Network — register institutions, view members, start focused discussions
- Compliance Tracker — document regulatory activities (NCISM, QCI, NAAC, NABH, etc.)
- Administrative Burden Calculator — quantify compliance costs in time and money
- Reform Proposal Generator — structured proposals with Current Situation, Solution, Benefits, Evidence, and Implementation sections
- Idea Board — post and upvote reform ideas

### 🔐 For Admin (Dr. Kembhavi)
- Dashboard with live statistics across all collections
- View and filter all private student feedback
- View faculty forum posts
- Moderate idea board (delete inappropriate posts)
- Create, manage, and close polls with live results
- View all network member registrations
- View all submitted reform proposals
- **Access Request Management** — approve or decline requests, auto-generate unique credentials, copy ready-to-send WhatsApp and email messages
- Export all student feedback as CSV
- Link to Analytics Dashboard (analytics.html)

### 📱 WhatsApp Integration
- Floating WhatsApp button on all pages
- Three pre-written shareable messages: Platform Invitation, Reform Discussion, Urgent Call to Action

### 🔒 Self-Registration System
- Visitors request access through the platform (no shared passwords)
- Admin reviews each request and approves or declines
- On approval: unique personal credentials are auto-generated
- Admin receives a copy-ready WhatsApp message and email message to forward directly to the user

---

## 🗂️ Repository Structure

```
ayurveda-unfiltered-voice/
│
├── index.html          ← Main platform (all features in one file)
├── analytics.html      ← Reform Analytics Dashboard (Chart.js)
└── README.md           ← This file
```

> **Note:** The previous `app.js`, `auth.js`, and `whatsapp-integration.js` files have been deprecated. All functionality is now embedded within `index.html`.

---

## 🔥 Firebase Collections

| Collection | Purpose | Access |
|---|---|---|
| `feedback` | Private student feedback | Write: public · Read: admin only |
| `ideas` | Public reform idea board | Read + Write: public |
| `polls` | Admin-created polls | Read: public · Write: admin only |
| `forumPosts` | Faculty discussion forum | Read + Write: public |
| `coalitionMembers` | Network institution registrations | Read + Write: public |
| `campaigns` | Focused discussion topics | Read + Write: public |
| `proposals` | Reform proposals submitted | Write: public · Read: admin only |
| `accessRequests` | Self-registration requests | Write: public · Read: admin only |
| `registeredUsers` | Approved user credentials | Read: public · Write: admin only |

---

## 🚀 Deployment

### Prerequisites
- A GitHub account
- A Google Firebase account (free tier is sufficient)

### Step 1 — Create Firebase Project
1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Create a new project named `ayurveda-unfiltered-voice`
3. Enable **Firestore Database** in Test Mode
4. Select region: `asia-south1` (Mumbai)

### Step 2 — Get Firebase Config
1. Project Settings → Your Apps → Add Web App
2. Copy the `firebaseConfig` object

### Step 3 — Configure index.html
Replace the placeholder config block in `index.html`:

```javascript
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT_ID.firebaseapp.com",
  projectId:         "YOUR_PROJECT_ID",
  storageBucket:     "YOUR_PROJECT_ID.appspot.com",
  messagingSenderId: "YOUR_SENDER_ID",
  appId:             "YOUR_APP_ID"
};
```

### Step 4 — Set Firestore Security Rules
In Firebase Console → Firestore → Rules, replace all content with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {

    match /feedback/{doc} {
      allow create: if true;
      allow read, update, delete: if false;
    }

    match /ideas/{doc} {
      allow read, create: if true;
      allow update: if request.resource.data.keys().hasOnly(['upvotes']);
      allow delete: if false;
    }

    match /polls/{doc} {
      allow read: if true;
      allow write: if false;
    }

    match /forumPosts/{doc} {
      allow read, create: if true;
      allow update: if request.resource.data.keys().hasOnly(['reactions']);
      allow delete: if false;
    }

    match /coalitionMembers/{doc} {
      allow read, create: if true;
      allow update, delete: if false;
    }

    match /campaigns/{doc} {
      allow read, create: if true;
      allow update, delete: if false;
    }

    match /proposals/{doc} {
      allow create: if true;
      allow read, update, delete: if false;
    }

    match /accessRequests/{doc} {
      allow create: if true;
      allow read, update, delete: if false;
    }

    match /registeredUsers/{doc} {
      allow create: if false;
      allow read: if true;
      allow update, delete: if false;
    }

  }
}
```

### Step 5 — Deploy on GitHub Pages
1. Create a new repository named `ayurveda-unfiltered-voice`
2. Upload `index.html` and `analytics.html`
3. Go to Settings → Pages → Deploy from branch → main → / (root)
4. Platform is live at `https://yourusername.github.io/ayurveda-unfiltered-voice`

---

## 🔑 Login & Registration System

### Two ways to access the platform

**1 — Preset shared credentials** (for general access, shared directly by Dr. Kembhavi)

| Role | Username | Password |
|---|---|---|
| UG Student | `ayurstudent2025` | `vaidya@123` |
| PG Scholar | `aypgscholar2025` | `pgvaidya@123` |
| Faculty / Professional | `ayurfaculty2025` | `faculty@ayur` |
| Admin | `ayuradmin2025` | `admin@vaidya` |

**2 — Self-registration via Firebase Authentication** (recommended for individual access)

Users register directly on the platform with their own email and chosen password:
- Visit the platform → click **Register Here →**
- Fill in: Full Name, Institution, State, Role, Email, Password, WhatsApp number
- **Email address becomes their username** — displayed clearly on the registration form
- **Live password strength indicator** guides them to choose a strong password
- Firebase Auth creates their account securely — password is never visible to anyone
- Their request appears in the Admin → Requests tab as **pending**
- On approval by Dr. Kembhavi, they can log in immediately with their email and password
- **Forgot Password** — fully automated: Firebase sends a reset link directly to their email, no admin involvement needed

### Authentication Architecture
- Preset credentials are checked first (hardcoded in JS, bypass Firebase Auth)
- Self-registered users authenticate via `firebase.auth().signInWithEmailAndPassword()`
- After Firebase Auth succeeds, approval status is verified in Firestore `accessRequests` collection
- Pending or declined users are signed out with an appropriate message
- Passwords are stored as secure cryptographic hashes by Firebase — nobody can read them

---

## 🛡️ Privacy & Security

- All private feedback is stored with Firebase security rules that prevent public reading
- Anonymous submission is the default for all student feedback
- PG Scholar confidential section is flagged as admin-eyes-only
- No shared passwords — every user through the Request Access system receives unique personal credentials
- The admin (Dr. Kembhavi) is the sole person with access to private submissions
- The platform does not use any advertising, tracking, or third-party analytics

---

## 🧰 Technology Stack

| Component | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript |
| Authentication | Firebase Authentication (Email/Password) |
| Database | Google Firebase Firestore |
| Hosting | GitHub Pages |
| Analytics Charts | Chart.js (analytics.html) |
| WhatsApp Integration | WhatsApp API (wa.me) |
| Storage (local) | Browser localStorage (compliance records, vote tracking) |

---

## 📊 Analytics Dashboard (analytics.html)

The analytics dashboard is a **separate, admin-login-protected** page that connects directly to Firebase and displays live real data. It is not accessible without the admin username and password.

**Access:** `https://yourusername.github.io/ayurveda-unfiltered-voice/analytics.html`
Or via: Admin Dashboard → Quick Actions → Analytics Dashboard

**Login required:** `ayuradmin2025` / `admin@vaidya`

### Live Charts (all powered by real Firebase data)
- Feedback by Category (bar chart)
- UG vs PG Submissions (doughnut)
- Student Rating Distribution (bar chart)
- Ideas by Category (doughnut)
- Forum Posts by Reform Category (bar chart)
- Access Requests Status — Pending / Approved / Declined (doughnut)
- Network Members by Location (bar chart)
- Active Poll Vote Results (bar chart)

### Live Data Tables
- Recent 10 feedback submissions with category, rating, and excerpt
- Top 10 upvoted ideas from the Idea Board
- Access requests summary with role and status badges

### PG Scholar Section Analysis
Visual breakdown of responses to the confidential PG section:
- Synopsis writing experience distribution
- Guide-scholar relationship quality
- Research infrastructure ratings

### Reform Movement Timeline
Auto-generated from real platform milestones — grows dynamically as the community grows.

### Report Generation (downloads real data)
- **Policy Impact Report** — formatted text file for submission to NCISM, educational boards, and policy makers
- **Reform Movement Summary** — overview with top ideas, forum categories, and movement statistics
- **Full Data Export** — complete JSON export of all Firebase collections for archival or analysis

### Technology
Built with Chart.js 3.9.1 via CDN and Firebase Firestore. No dummy or hardcoded data — all numbers reflect actual platform activity.

---

## 🔄 Version History

| Version | Description |
|---|---|
| v1.0 | Original AyurVoice — student feedback platform with Firebase |
| v2.0 | Merged platform — added faculty forum, compliance tracker, reform proposals, WhatsApp integration |
| v3.0 | Full unified platform — self-registration system, auto-generated credentials, WhatsApp + email credential sharing, pending request notifications |
| v3.1 | Analytics dashboard rebuilt — admin-login-protected, all dummy data removed, live Firebase charts and real data tables |
| v3.2 | Firebase Authentication integrated — users register with their own email and password, automated Forgot Password, live password strength indicator, admin approval workflow |

---

## 📬 Contact & Contribution

**Dr. Aakash Kembhavi**  
MD Ayurveda | MS Counselling & Psychotherapy  
Principal, Jain AGM Ayurvedic Medical College & Hospital, Varur  
Director of PG Studies, SJG Ayurvedic Medical College, Koppal  
PhD Guide, RGUHS | Chief Editor, International Journal of Ayurveda  

📝 Blog: [drkembhavi-s.github.io](https://drkembhavi-s.github.io)  
🌿 Platform: (https://DrKembhavi-s.github.io/ayurveda-unfiltered-voice)  

---

## 📄 Licence

This platform was developed for the Ayurveda reform community. You are welcome to fork and adapt it for similar educational reform initiatives with attribution.

---

*"The silence in Ayurveda institutions is not inevitable. It is a choice — and it can be unchosen."*
