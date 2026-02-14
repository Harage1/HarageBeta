# Harage - Professional Blog Platform
**Version:** 1.0.0 | **Status:** Production-Ready | **LB4 Company Official Project**

---

## 📋 Project Overview

Harage is a modern, responsive blog platform featuring multi-language support (Arabic, English, French), dark mode, and a professional Firebase-backed content management system. The platform emphasizes clean design, accessibility, and performance.

**Key Features:**
- 📱 Fully responsive design (mobile-first approach)
- 🌙 Dark/Light mode toggle with persistence
- 🌍 Multi-language support (AR/EN/FR) with i18n system
- 🔐 Admin panel with password protection (password: `7744`)
- 📚 Firebase Firestore backend for article management
- 🎨 Professional B&W minimalist design aesthetic
- ⚡ Vanilla HTML5 + JavaScript (no framework dependencies)
- 🔄 Automatic fallback to localStorage for offline support

---

## 🏗️ Project Architecture

### Technology Stack

**Frontend:**
- Pure HTML5 + Vanilla JavaScript
- Inline CSS with CSS custom properties
- Responsive media queries (768px tablet, 480px mobile breakpoints)
- No build process required for production

**Backend:**
- **Firebase Firestore** (Cloud Database)
  - Project ID: `harage-c5dd1`
  - Real-time article sync
  - Automatic offline fallback

**Internationalization (i18n):**
- Universal data-* attribute system
- Languages: Arabic (AR), English (EN), French (FR)
- localStorage persistence for user language preference

**Session Management:**
- Dark mode: localStorage `harage_dark_mode` toggle
- Language: localStorage `harage_language` 
- Intro modal: Shows every page load, auto-hides after 7 seconds

### Codebase Structure

```
Harage/
├── 📄 README.md                    (Project documentation - THIS FILE)
├── 📄 index.html                   (Homepage - 818 lines)
│   ├── Featured article section (2-column responsive layout)
│   ├── Article grid display (latest 6 articles)
│   ├── Header with logo, nav, dark mode, language switcher
│   └── Intro modal (welcome message)
│
├── 📄 articles.html                (Article listing page - 476 lines)
│   ├── Category filter buttons
│   ├── Full article grid with sorting
│   └── Responsive layout
│
├── 📄 article-detail.html          (Single article page - 551 lines)
│   ├── Article title, image, metadata
│   ├── Related articles section
│   └── Back button navigation
│
├── 📄 credits.html                 (Team/About page - 544 lines)
│   ├── Team member cards
│   ├── Technology stack information
│   └── Professional company information
│
├── 📄 admin.html                   (Admin panel - 445 lines)
│   ├── Password authentication (7744)
│   ├── CRUD article management interface
│   ├── Article creation/editing/deletion
│   └── Responsive admin dashboard
│
├── 🎨 logo.png                     (44px rounded logo)
│
├── 📦 package.json                 (Project metadata)
│   └── **Note: See ARCHITECTURE NOTES below**
│
└── 📁 js/
    ├── data.js                     (PRIMARY - Firebase operations)
    │   ├── Firebase initialization via CDN
    │   ├── Global functions: getAllArticles, getArticleById, 
    │   │                     addNewArticle, deleteArticle, updateArticle
    │   └── Offline fallback with localStorage
    │
    ├── admin.js                    (Admin panel Firebase operations)
    │   ├── Separate Firebase init (mirrors data.js)
    │   ├── CRUD operations for article management
    │   └── Form submission handling
    │
    ├── translations.json           (⚠️ UNUSED - see i18n section)
    ├── i18n.js                     (⚠️ UNUSED - see i18n section)
    ├── home.js                     (⚠️ UNUSED - index.html self-contained)
    ├── articles.js                 (⚠️ UNUSED - articles.html self-contained)
    ├── article-detail.js           (⚠️ UNUSED - article-detail.html self-contained)
    └── add-article.js              (⚠️ UNUSED - add-article.html orphaned)
```

---

## 🚀 Setup & Installation

### Prerequisites
- Node.js 16+ (for http-server)
- Modern web browser (Chrome, Firefox, Safari, Edge)
- API access to harage-c5dd1 Firebase project

### Development Setup

1. **Clone/Extract Project**
   ```bash
   cd ~/Desktop/Harage
   ```

2. **Start Development Server**
   ```bash
   npm install
   npx http-server -p 3000 --cors
   ```

3. **Access Application**
   - Homepage: http://localhost:3000
   - Articles: http://localhost:3000/articles.html
   - Admin Panel: http://localhost:3000/admin.html (password: 7744)

4. **Configuration**
   - Firebase credentials are embedded in `js/data.js` and `js/admin.js`
   - See SECURITY NOTES for production recommendations

---

## 🌍 Internationalization (i18n)

### Language System

The project uses a **data-* attribute system** for translations:

```html
<h2 data-ar="أحدث المقالات" data-en="Latest Articles" data-fr="Derniers Articles">
  أحدث المقالات
</h2>
```

**Implementation:**
- Language preference stored in localStorage: `harage_language`
- Default language: Arabic (AR)
- Supported languages: English (EN), French (FR)
- RTL/LTR handled automatically based on language

**Language Switcher:**
Located in header - dropdown showing عربي / English / Français

**Translation Coverage:**
- All page titles and UI text
- Navigation elements
- Button labels
- Section headers
- User-facing messages

### Setting User Language

Users select language from dropdown in header:
- Selection persists via localStorage
- Page automatically updates all data-* attributes
- Direction (RTL/LTR) updates automatically

---

## 🎨 Design System

### Typography

- **Font Family:** System fonts (-apple-system, BlinkMacSystemFont, 'Segoe UI')
- **Page Titles:** 2.8rem, 700 weight, -0.5px letter-spacing
- **Section Headers:** 1.6rem, 700 weight, bottom border
- **Body:** 1rem, 1.6 line-height
- **Responsive:** Scales down at 768px (tablet) and 480px (mobile)

### Color Palette

```css
:root {
  --bg-light: #ffffff;           /* Light mode background */
  --bg-dark: #000000;            /* Dark mode background */
  --text-light: #000000;         /* Light mode text */
  --text-dark: #ffffff;          /* Dark mode text */
  --border-light: #e5e5e5;       /* Light mode borders */
  --border-dark: #333333;        /* Dark mode borders */
  --hover-light: #f5f5f5;        /* Light mode hover */
  --hover-dark: #1a1a1a;         /* Dark mode hover */
}
```

**Color Scheme:** Pure black & white (no color accents)

### Component Styles

**Article Cards:**
- Border-radius: 12px (modern rounded corners)
- Box-shadow: 0 4-12px rgba(0,0,0,0.08-0.15)
- Transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1)
- Hover effect: translateY(-6px) with enhanced shadow
- Grid: auto-fill, minmax(320px, 1fr)

**Featured Section (Homepage):**
- Desktop: 2-column layout (1.4fr 1fr)
- Mobile: Single column (100%)
- Image height: 320px (desktop), 240px (tablet), 200px (mobile)

**Navigation Header:**
- Sticky positioning (top: 0)
- Z-index: 50
- Logo: 44px height, rounded border
- Dark/Light mode toggle button
- Language switcher dropdown

---

## 🔐 Security & Credentials

⚠️ **CURRENT SECURITY STATUS: REQUIRES REMEDIATION FOR PRODUCTION**

### Firebase Configuration

**Current Implementation:**
- API key hardcoded in `js/data.js` and `js/admin.js`
- Firebase configuration exposed in source code
- Credentials visible in browser DevTools

**Firebase Credentials:**
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyDO9tGjUT-YPtvEFbc4ZBkVJF4UgaXCdOE",
  authDomain: "harage-c5dd1.firebaseapp.com",
  projectId: "harage-c5dd1",
  storageBucket: "harage-c5dd1.firebasestorage.app",
  messagingSenderId: "179223858199",
  appId: "1:179223858199:web:fbf2e5ab8cc0b763cca052",
  measurementId: "G-XDXN5GGM37"
};
```

### ⚠️ SECURITY ISSUE: API Key Exposure

**Risk Level:** CRITICAL
- API keys are client-side (technically public in web apps)
- Firebase Security Rules MUST protect sensitive operations
- Currently no Security Rules implemented

### Recommended Security Actions

1. **Implement Firebase Security Rules**
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /articles/{document=**} {
         allow read: if true;  // Articles readable by anyone
         allow write: if request.auth != null && 
                         request.auth.customClaims.admin == true;  // Only admins write
       }
     }
   }
   ```

2. **Admin Authentication Enhancement**
   - Replace password-only auth with Firebase Authentication
   - Use Firebase Admin SDK on backend
   - Implement JWT token verification

3. **Environment Variables (Long-term)**
   - Move config to `.env` file
   - Use build process (Vite) to inject at compile time
   - Never commit `.env` to version control

---

## 📚 API Reference

### Global Window Functions (from data.js)

All Firebase operations are exposed as global functions:

#### `getAllArticles()`
Returns all articles from Firestore
```javascript
const articles = await window.getAllArticles();
// Returns: Array of article objects with id, title, description, etc.
```

#### `getArticleById(id)`
Retrieves single article by ID
```javascript
const article = await window.getArticleById('article-id-123');
// Returns: Article object or null if not found
```

#### `addNewArticle(articleData)`
Creates new article in Firestore
```javascript
await window.addNewArticle({
  title: "Article Title",
  description: "Article description",
  category: "Technology",
  imageUrl: "https://example.com/image.jpg",
  content: "Full article content..."
});
```

#### `deleteArticle(id)`
Removes article from Firestore
```javascript
await window.deleteArticle('article-id-123');
```

#### `updateArticle(id, articleData)`
Updates existing article
```javascript
await window.updateArticle('article-id-123', {
  title: "Updated Title",
  description: "Updated description"
});
```

### Admin Panel Functions (from admin.js)

Separate Firebase initialization for admin operations (see admin.html for usage)

---

## 🚀 Deployment Guide

### Prerequisites
- Firebase project configured (harage-c5dd1)
- Node.js installed
- Domain/hosting selected

### Local Production Build

```bash
npm install
npx http-server -p 3000 --cors
```

### Cloud Deployment Options

**Option A: Firebase Hosting**
```bash
npm install -g firebase-tools
firebase login
firebase deploy --project harage-c5dd1
```

**Option B: Vercel**
```bash
npm install -g vercel
vercel
```

**Option C: Netlify**
```bash
npm install -g netlify-cli
netlify deploy
```

### Pre-Deployment Checklist

- [ ] Test all pages in production environment
- [ ] Verify Firebase connection
- [ ] Test admin panel authentication
- [ ] Test all languages (AR/EN/FR)
- [ ] Test dark/light mode toggle
- [ ] Test mobile responsiveness
- [ ] Verify all external assets load
- [ ] Check browser console for errors
- [ ] Test offline fallback (localStorage)
- [ ] Performance audit (Lighthouse)
- [ ] Security audit (OWASP)

---

## 🐛 Troubleshooting

### Firebase Connection Issues

**Problem:** "Firebase is not initialized" in console

**Solution:** 
- Ensure internet connection
- Check Firebase project status
- Verify firebaseConfig credentials
- Check browser console for specific errors
- localStorage fallback will activate automatically

### Articles Not Loading

**Problem:** Articles grid appears empty

**Solution:**
- Check Firebase Firestore for articles collection
- Verify articles have required fields: title, description, category
- Check browser DevTools Network tab for Firebase requests
- Check localStorage for cached articles

### Language/i18n Not Working

**Problem:** Switching language doesn't translate page

**Solution:**
- Verify data-ar, data-en, data-fr attributes present on elements
- Check localStorage for 'harage_language' key
- Refresh page after language change
- Check browser DevTools Console for i18n errors

### Dark Mode Not Persisting

**Problem:** Dark mode resets on page reload

**Solution:**
- Check localStorage for 'harage_dark_mode' key
- Verify localStorage not disabled in browser
- Check browser privacy settings
- Clear browser cache and try again

### Admin Panel Authentication Issues

**Problem:** Wrong password message or admin panel not loading

**Solution:**
- Default admin password: `7744`
- Check that admin.html is accessible
- Verify admin.js is loaded (Network tab)
- Check browser console for JavaScript errors
- Clear browser cache and retry

---

## 📊 Performance Notes

### Current Performance Characteristics

- **Page Load:** < 2 seconds (with Firebase)
- **Fallback (localhost):** < 500ms with localStorage
- **CSS Load:** Inline (no external stylesheets after initial page load)
- **Image Optimization:** Lazy loading with onerror fallback

### Optimization Opportunities

1. **Image Optimization**
   - Implement webp format
   - Add responsive image sizes
   - Use CDN for image delivery

2. **Caching Strategy**
   - Implement service worker
   - Add aggressive cache headers
   - Use versionable asset names

3. **Code Splitting**
   - Lazy load admin functionality
   - Separate article detail code
   - Code splitting per page

4. **Bundle Size**
   - Currently ~2-4KB HTML per page
   - ~5KB Firebase CDN import
   - CSS: ~8-12KB inline per page

---

## 🔄 Maintenance & Updates

### Regular Tasks

**Weekly:**
- Monitor Firebase usage and costs
- Check for article submission errors
- Verify admin panel functionality

**Monthly:**
- Review Firebase security rules
- Update browser compatibility testing
- Audit analytics data

**Quarterly:**
- Content review and cleanup
- Performance benchmarking
- Security audit

### Version Management

**Current Version:** 1.0.0

To increment version:
```bash
npm version patch    # 1.0.0 → 1.0.1
npm version minor    # 1.0.0 → 1.1.0
npm version major    # 1.0.0 → 2.0.0
```

---

## 📝 Architecture Notes

### IMPORTANT: Tooling vs. Implementation Mismatch

**Current Status:**

The `package.json` file declares the following dependencies and tools:
- React 18.2.0
- Vite (build runner)
- TailwindCSS
- PostCSS
- react-router-dom

**However:** NONE of these are actually used in the current codebase.

**Actual Implementation:**
- Pure HTML5 + Vanilla JavaScript
- Inline CSS (no TailwindCSS)
- No build process (no Vite)
- No React or routing library

**Why This Mismatch?**
The project was originally scaffolded with these tools for future flexibility but now uses a simpler vanilla approach. The dependencies are installed but not active.

### Options for Alignment

**Option A: Keep Vanilla Architecture (Current)**
- Remove React, Vite, TailwindCSS from package.json
- Keep current simple approach
- Benefits: Fast, lightweight, no build step
- Continue using ES6 modules only in js/data.js

**Option B: Migrate to Vite + React**
- Implement proper component structure
- Use TailwindCSS for styling
- Add build process
- Benefits: Better scalability, component reuse, modern tooling
- More complex deployment
- Higher dev dependency footprint

**Recommendation:** For current production state, Option A (cleanup) is preferred. Option B should be considered for major version 2.0 if complexity increases significantly.

---

## 📄 File Inventory & Status

### Active Files (Used in Production)
- ✅ index.html - Homepage
- ✅ articles.html - Article listing
- ✅ article-detail.html - Article viewer
- ✅ credits.html - Team/About
- ✅ admin.html - Admin panel
- ✅ js/data.js - Firebase operations (main system)
- ✅ js/admin.js - Admin Firebase operations
- ✅ logo.png - Brand logo
- ✅ package.json - Project metadata

### Unused Files (Should be Cleaned Up)
- ❌ add-article.html - No navigation link, purpose unclear
- ❌ add-article.js - Orphaned companion file
- ❌ home.js - Duplicate of index.html functionality (ES6 module)
- ❌ articles.js - Duplicate of articles.html functionality (ES6 module)
- ❌ article-detail.js - Duplicate of article-detail.html (ES6 module)
- ❌ i18n.js - Alternative i18n system (not used, data-* used instead)
- ❌ translations.json - Alternative translation file (not used)
- ❌ justfordesing.html - Reference file (hajir.ma design analysis)

**Cleanup Status:** Pending in Phase 8 production audit

---

## 🤝 Contributing & Development

### Development Workflow

1. **Make changes** to HTML/CSS/JS files
2. **Test locally** via http://localhost:3000
3. **Verify** in multiple browsers and devices
4. **Check console** for errors (F12)
5. **Test all languages** (AR/EN/FR)
6. **Test dark mode** toggle
7. **Commit changes**

### Code Style Guidelines

**HTML:**
- Use semantic elements (header, nav, main, article, section)
- Add lang attribute to html element
- Include data-* attributes for translations

**CSS:**
- Use CSS custom properties for colors
- Include dark mode media query support
- Test responsive breakpoints (768px, 480px)

**JavaScript:**
- Use strict mode ('use strict')
- Use modern ES6 syntax (const/let, arrow functions)
- Include try-catch error handling
- Add console logging for debugging

---

## 📞 Support & Documentation

For questions or issues:
1. Check TROUBLESHOOTING section above
2. Review browser console errors (F12)
3. Check Firebase status page
4. Review this README documentation

---

**Last Updated:** February 8, 2026  
**Project Lead:** LB4 Company  
**Status:** Production-Ready (with security remediation recommended)
