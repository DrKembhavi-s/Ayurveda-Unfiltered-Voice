# 🌿 Dr. Kembhavi's Ayurveda Unfiltered Voice

> *A confidential, Firebase-secured platform for reform voices in Ayurveda education — Academic, Clinical, Research, Administrative, and Development.*

**Live Platform:** [https://drkembhavi-s.github.io/ayurveda-unfiltered-voice](https://drkembhavi-s.github.io/ayurveda-unfiltered-voice)  
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
4. Platform is live at `https://drkembhavi-s.github.io/ayurveda-unfiltered-voice`

---

## 🔑 Login Credentials

### Preset Credentials (for direct sharing)

| Role | Username | Password |
|---|---|---|
| UG Student | `ayurstudent2025` | `vaidya@123` |
| PG Scholar | `aypgscholar2025` | `pgvaidya@123` |
| Faculty / Professional | `ayurfaculty2025` | `faculty@ayur` |
| Admin | `ayuradmin2025` | `admin@vaidya` |

### Self-Registered Users
Users who apply through the **Request Access** system receive auto-generated personal credentials in the format:
- **Username:** `firstname_role_4digitnumber` (e.g. `suresh_pg_4821`)
- **Password:** `6randomchars@ayur` (e.g. `kx7r2m@ayur`)

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
| Database | Google Firebase Firestore |
| Hosting | GitHub Pages |
| Analytics Charts | Chart.js (analytics.html) |
| WhatsApp Integration | WhatsApp API (wa.me) |
| Storage (local) | Browser localStorage (compliance records only) |

---

## 📊 Analytics Dashboard

The separate `analytics.html` file provides a data visualisation dashboard with:
- Movement growth charts (Chart.js)
- Issue category distribution
- Regulatory body impact analysis
- Time distribution charts
- State-wise participation data
- Report generation for policy submission

Access it directly at: `https://drkembhavi-s.github.io/ayurveda-unfiltered-voice/analytics.html`
Or via the admin dashboard → Quick Actions → Analytics Dashboard.

---

## 🔄 Version History

| Version | Description |
|---|---|
| v1.0 | Original AyurVoice — student feedback platform with Firebase |
| v2.0 | Merged platform — added faculty forum, compliance tracker, reform proposals, WhatsApp integration |
| v3.0 | Full unified platform — self-registration system, auto-generated credentials, WhatsApp + email credential sharing, pending request notifications |

---

## 📬 Contact & Contribution

**Dr. Aakash Kembhavi**  
MD Ayurveda | MS Counselling & Psychotherapy  
Principal, Jain AGM Ayurvedic Medical College & Hospital, Varur  
Director of PG Studies, SJG Ayurvedic Medical College, Koppal  
PhD Guide, RGUHS | Chief Editor, International Journal of Ayurveda  

📝 Blog: [drkembhavi-s.github.io](https://drkembhavi-s.github.io)  
🌿 Platform: (https://drkembhavi-s.github.io/Ayurveda-Unfiltered-Voice/)

---

## 📄 Licence

This platform was developed for the Ayurveda reform community. You are welcome to fork and adapt it for similar educational reform initiatives with attribution.

---

*"The silence in Ayurveda institutions is not inevitable. It is a choice — and it can be unchosen."*
