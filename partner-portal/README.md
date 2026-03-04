# Stonnex Partner Portal

Password-protected document sharing portal for Stonnex Group. Not linked from the main site.

---

## Setup (one time, ~5 minutes)

### 1. Create a new GitHub repo

Go to https://github.com/new and create:
- **Repository name:** `stonnex-partner`
- **Visibility:** Private (recommended) or Public
- Do NOT initialize with README

### 2. Push this folder to the new repo

Open Terminal and run:

```bash
cd /path/to/partner-portal
git init
git add .
git commit -m "Initial portal setup"
git remote add origin https://github.com/crasode/stonnex-partner.git
git push -u origin main
```

### 3. Enable GitHub Pages

1. Go to your new repo on GitHub
2. Settings → Pages
3. Source: Deploy from branch → `main` → `/` (root)
4. Save

Your portal will be live at: `https://crasode.github.io/stonnex-partner`

### 4. (Optional) Set up a custom subdomain like `partner.stonnex.com`

1. In the repo, create a file called `CNAME` containing just:
   ```
   partner.stonnex.com
   ```
2. In your domain registrar (wherever stonnex.com is managed), add a DNS record:
   - Type: `CNAME`
   - Name: `partner`
   - Value: `crasode.github.io`
3. Back in GitHub Pages settings, enter `partner.stonnex.com` as the custom domain
4. Check "Enforce HTTPS"

---

## Adding a New Document

### Step 1 — Upload the file

Upload your HTML or PDF to the `/docs/` folder on GitHub:
- GitHub repo → `docs/` folder → "Add file" → "Upload files"

### Step 2 — Add an entry to the document list

Open `index.html` and find the `DOCUMENTS` array (around line 60). Add a new entry:

```javascript
{
  id:          3,                              // next number in sequence
  title:       "Your Document Title",
  description: "One sentence about what this contains.",
  type:        "html",                         // "html" or "pdf"
  url:         "docs/your-filename.html",      // relative path to the file
  category:    "Marketing",                   // Marketing | Brand | Financial | Strategy | Operations
  date:        "2026-03-10",                  // date added YYYY-MM-DD
  isNew:       true                           // set false after first week
}
```

Commit the change and the document appears in the portal immediately.

---

## Changing the Password

1. Go to https://emn178.github.io/online-tools/sha256.html
2. Type your new password and copy the hash
3. Open `index.html`, find `const PASSWORD_HASH = "..."` and replace the hash
4. Commit and push

**Current default password:** `stonnex2026`

---

## File structure

```
partner-portal/
├── index.html          ← Portal app (login + dashboard)
├── CNAME               ← Custom domain (if using subdomain)
├── README.md           ← This file
└── docs/
    ├── Stonnex_Social_Calendar_March2026_Visual.html
    ├── Stonnex_Social_Calendar_March2026.html
    └── [future documents go here]
```

---

## Notes

- The portal is client-side only — password verification happens in the browser using SHA-256 hashing. This is appropriate for sharing documents with a trusted partner but is not designed for highly sensitive data.
- Session persists within the browser tab. Closing the tab requires re-entry of the password.
- No backend, no database, no subscription fees — runs entirely on GitHub Pages (free).
