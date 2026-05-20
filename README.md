# 📖 THE VISUAL DIARY
### *A quiet space for thoughts, memories, and moments.*

A luxury digital scrapbook journal — built with React, Node.js, Express, MySQL, Tailwind CSS, and Framer Motion.

---

## ✦ Stack

| Layer     | Technology                             |
|-----------|----------------------------------------|
| Frontend  | React 18, Tailwind CSS 3, Framer Motion |
| Backend   | Node.js v14, Express.js                |
| Database  | MySQL                                  |
| Auth      | JWT + bcryptjs                         |
| Uploads   | Multer (local file storage)            |
| Fonts     | Playfair Display, Cormorant Garamond, Caveat, DM Sans |

---

## ✦ Project Structure

```
visual-diary/
├── backend/
│   ├── server.js              # Express entry point
│   ├── .env.example           # Environment variables template
│   ├── package.json
│   ├── config/
│   │   └── db.js              # MySQL connection pool
│   ├── middleware/
│   │   └── auth.js            # JWT middleware
│   ├── routes/
│   │   ├── auth.js            # signup / login / me
│   │   ├── entries.js         # CRUD + stats + calendar
│   │   ├── profile.js         # profile + image upload
│   │   └── settings.js        # user settings + themes
│   ├── uploads/               # uploaded images (auto-created)
│   └── database/
│       └── schema.sql         # Full MySQL schema
│
└── frontend/
    ├── package.json
    ├── tailwind.config.js
    ├── postcss.config.js
    ├── public/
    │   └── index.html         # Google Fonts loaded here
    └── src/
        ├── index.js
        ├── App.jsx            # Routes
        ├── index.css          # All custom CSS (textures, polaroids, tape, etc.)
        ├── context/
        │   └── AuthContext.jsx
        ├── components/
        │   ├── AppLayout.jsx  # Sidebar + main wrapper
        │   └── Sidebar.jsx
        └── pages/
            ├── Landing.jsx    # Cinematic editorial landing
            ├── Login.jsx
            ├── Signup.jsx
            ├── Dashboard.jsx  # Aesthetic non-corporate overview
            ├── Editor.jsx     # ✦ THE HEART — visual journal editor
            ├── AllEntries.jsx # Card grid with search & filters
            ├── Calendar.jsx   # Monthly memory calendar
            ├── Profile.jsx    # Beautiful profile + gallery
            └── Settings.jsx   # Themes, preferences, password
```

---

## ✦ Setup Instructions

# 1. REQUIREMENTS

Install these first:

| Software              | Version  |
| --------------------- | -------- |
| Node.js               | v14.21.3 |
| MySQL                 | 8.x      |
| VS Code (recommended) | Latest   |

---

# 2. INSTALL NODE.JS

Download:

[https://nodejs.org/en/download](https://nodejs.org/en/download)

Install:

* Download `.msi` installer
* Click Next → Next → Install
* Finish

## VERIFY INSTALLATION

Open CMD:

```bash
node -v
npm -v
```

If installed correctly:

```bash
v14.21.3
```

---

# 3. INSTALL MYSQL

Download:

[https://dev.mysql.com/downloads/mysql/](https://dev.mysql.com/downloads/mysql/)

Install:

* Choose:

```txt
Developer Default
```

During installation:

* Create root password
* REMEMBER PASSWORD

Example:

```txt
1234
```

Finish installation.

---

# 4. FIX MYSQL COMMAND NOT RECOGNIZED

## Problem

```bash
'mysql' is not recognized as an internal or external command
```

## Cause

MySQL `bin` folder is not added to Windows PATH.

---

## Temporary Fix

Use full MySQL path:

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe"
```

Example:

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe" -u root -p
```

---

## Permanent Fix (Recommended)

Copy this path:

```txt
C:\Program Files\MySQL\MySQL Server 8.0\bin
```

Then:

1. Windows Search
2. Search:

```txt
Environment Variables
```

3. Open:

```txt
Edit the system environment variables
```

4. Click:

```txt
Environment Variables
```

5. Under System Variables:

* Select `Path`
* Click Edit

6. Click New

7. Paste:

```txt
C:\Program Files\MySQL\MySQL Server 8.0\bin
```

8. Press OK everywhere

9. Restart terminal

Now this should work:

```bash
mysql -u root -p
```

---

# 5. PROJECT LOCATION

Example project path:

```txt
C:\Users\Kamal G\Desktop\yojak\projects\visual-diary
```

---

# 6. OPEN PROJECT IN TERMINAL

Open CMD.

Go to project:

```bash
cd Desktop
cd yojak
cd projects
cd visual-diary
```

---

# 7. CREATE DATABASE

Open MySQL:

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe" -u root -p
```

Enter password.

Inside MySQL:

```sql
CREATE DATABASE visual_diary;
```

Then:

```sql
exit;
```

---

# 8. IMPORT SCHEMA

Go backend:

```bash
cd backend
```

Run:

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe" -u root -p visual_diary < database\schema.sql
```

---

# 9. FIX SCHEMA ERROR

## Problem

```bash
ERROR 1136 (21S01): Column count doesn't match value count at row 2
```

## Cause

`themes` insert query had missing `FALSE` values.

---

## FIXED QUERY

Replace the themes insert block with:

```sql
INSERT IGNORE INTO themes (name, display_name, background_color, text_color, accent_color, font_family, description, is_default) VALUES
('vintage-paper', 'Vintage Paper', '#F5F0E8', '#2C2C2C', '#8B7355', 'Cormorant Garamond', 'Warm, aged paper aesthetic', TRUE),
('soft-beige', 'Soft Beige', '#FAF6F0', '#3D3530', '#C4A882', 'Playfair Display', 'Gentle cream tones', FALSE),
('dotted-notebook', 'Dotted Notebook', '#FAFAFA', '#2D2D2D', '#6B8F71', 'Caveat', 'Classic dotted journal style', FALSE),
('minimal-white', 'Minimal White', '#FFFFFF', '#1A1A1A', '#B0927A', 'Inter', 'Clean, modern minimal', FALSE),
('dark-journal', 'Dark Journal', '#1C1917', '#F5F0E8', '#C4A882', 'Cormorant Garamond', 'Moody, night writing', FALSE);
```

Save file.

Then rerun schema import.

---

# 10. BACKEND SETUP

Go backend:

```bash
cd backend
```

Install dependencies:

```bash
npm install
```

Create uploads folder:

```bash
mkdir uploads
```

Create `.env` file:

```bash
copy .env.example .env
```

---

# 11. FIX .ENV FILE ISSUES

## Problem

Windows asks:

```txt
Choose app to open .env
```

## Solution

DO NOT double-click `.env`.

Right click:

```txt
Open With → Notepad
```

OR use VS Code.

---

## Important

Make sure file is named:

```txt
.env
```

NOT:

```txt
.env.txt
```

Enable file extensions:

```txt
View → File name extensions
```

---

# 12. ENV FILE CONTENT

Paste this:

```env
PORT=5000
CLIENT_URL=http://localhost:3000

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=YOUR_PASSWORD
DB_NAME=visual_diary

JWT_SECRET=mysecretkey123
```

Replace:

```txt
YOUR_PASSWORD
```

with your MySQL password.

Example:

```env
DB_PASSWORD=1234
```

Save file.

---

# 13. START BACKEND

Inside backend:

```bash
npm run dev
```

Expected:

```bash
Connected to MySQL
Server running on port 5000
```

---

# 14. FRONTEND SETUP

Open SECOND terminal.

Go frontend:

```bash
cd Desktop
cd yojak
cd projects
cd visual-diary
cd frontend
```

Install dependencies:

```bash
npm install
```

Start frontend:

```bash
npm start
```

---

# 15. OPEN APP

Browser should open automatically.

If not:

```txt
http://localhost:3000
```

---

# 16. COMPLETE STARTUP FLOW (FUTURE USE)

Whenever reopening project:

---

## START BACKEND

Terminal 1:

```bash
cd Desktop
cd yojak
cd projects
cd visual-diary
cd backend
npm run dev
```

---

## START FRONTEND

Terminal 2:

```bash
cd Desktop
cd yojak
cd projects
cd visual-diary
cd frontend
npm start
```

---

# 17. MYSQL QUICK CHECK QUERIES

Use these queries to inspect and debug database data.

---

## Open MySQL

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe" -u root -p
```

---

## Select Database

```sql
USE visual_diary;
```

---

## Show All Tables

```sql
SHOW TABLES;
```

---

## Show Structure of Table

Example:

```sql
DESCRIBE users;
```

or:

```sql
DESC users;
```

---

## Check Registered Users

```sql
SELECT * FROM users;
```

---

## Check Journal Entries

```sql
SELECT * FROM journal_entries;
```

---

## Check Themes

```sql
SELECT * FROM themes;
```

---

## Check User Settings

```sql
SELECT * FROM user_settings;
```

---

## Count Total Users

```sql
SELECT COUNT(*) FROM users;
```

---

## Count Total Journal Entries

```sql
SELECT COUNT(*) FROM journal_entries;
```

---

## Show Latest Entries

```sql
SELECT * FROM journal_entries ORDER BY created_at DESC LIMIT 5;
```

---

## Delete All Users

```sql
DELETE FROM users;
```

---

## Delete All Journal Entries

```sql
DELETE FROM journal_entries;
```

---

## Drop Entire Database

WARNING: Deletes everything.

```sql
DROP DATABASE visual_diary;
```

---

## Recreate Database

```sql
CREATE DATABASE visual_diary;
```

---

## Exit MySQL

```sql
exit;
```

---

# 18. COMMON ERRORS + FIXES

---

## ERROR

```bash
'mysql' is not recognized
```

### FIX

Use full MySQL path OR add MySQL to PATH.

---

## ERROR

```bash
Unknown database 'visual_diary'
```

### FIX

Create database:

```sql
CREATE DATABASE visual_diary;
```

---

## ERROR

```bash
Column count doesn't match value count
```

### FIX

Fix themes insert query.

---

## ERROR

```bash
Choose app to open .env
```

### FIX

Open with Notepad or VS Code.

---

## ERROR

```bash
.env not working
```

### FIX

Check file is named:

```txt
.env
```

NOT:

```txt
.env.txt
```

---

## ERROR

```bash
ECONNREFUSED
```

### FIX

MySQL service is not running.

Start MySQL service.

---

## ERROR

```bash
npm is not recognized
```

### FIX

Reinstall Node.js.

Restart PC.

---

## ERROR

```bash
Module not found
```

### FIX

Run:

```bash
npm install
```

inside correct folder.

---

# 19. IMPORTANT PROJECT PORTS

| Service  | Port |
| -------- | ---- |
| Frontend | 3000 |
| Backend  | 5000 |
| MySQL    | 3306 |

---

# 20. PROJECT STRUCTURE

```txt
visual-diary/
│
├── backend/
│   ├── database/
│   ├── routes/
│   ├── uploads/
│   ├── .env
│   └── server.js
│
└── frontend/
    ├── src/
    └── package.json
```

---

# 21. FINAL CHECKLIST

Before running:

```txt
✅ Node.js installed
✅ MySQL installed
✅ Database created
✅ schema.sql imported
✅ backend/.env exists
✅ uploads folder exists
✅ npm install done in backend
✅ npm install done in frontend
```

---

# 22. QUICK COMMAND REFERENCE

## Backend

```bash
cd backend
npm run dev
```

---

## Frontend

```bash
cd frontend
npm start
```

---

## Open MySQL

```bash
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql.exe" -u root -p
```

---

# 23. APP URL

```txt
http://localhost:3000
```

---

# 24. IMPORTANT WINDOWS NOTES

## Windows Command Differences

Windows uses:

```bash
copy .env.example .env
```

Linux/Mac uses:

```bash
cp .env.example .env
```

---

## Windows Upload Folder Command

Windows:

```bash
mkdir uploads
```

Linux/Mac:

```bash
mkdir -p uploads
```

---

## Always Run Backend First

Start backend before frontend.

Otherwise frontend may show API/network errors.

---

## Backend Terminal Must Stay Open

Do NOT close backend terminal while app is running.

---

## Recommended Tools

| Tool            | Purpose         |
| --------------- | --------------- |
| VS Code         | Code editor     |
| MySQL Workbench | Database viewer |
| Postman         | API testing     |
| Git Bash        | Better terminal |

---

# DONE

## ✦ Pages Overview

| Page       | Route           | Description                          |
|------------|-----------------|--------------------------------------|
| Landing    | `/`             | Cinematic editorial hero page        |
| Login      | `/login`        | Paper card login form                |
| Signup     | `/signup`       | Paper card signup form               |
| Dashboard  | `/dashboard`    | Stats, recent entries, mini calendar |
| Editor     | `/editor`       | Visual scrapbook journal editor      |
| Edit Entry | `/editor/:id`   | Edit an existing entry               |
| All Entries| `/entries`      | Card grid with search & mood filters |
| Calendar   | `/calendar`     | Monthly memory timeline              |
| Profile    | `/profile`      | Profile stats, gallery, bio          |
| Settings   | `/settings`     | Themes, preferences, password        |

---

## ✦ API Endpoints

### Auth
```
POST   /api/auth/signup     — Register new user
POST   /api/auth/login      — Login
GET    /api/auth/me         — Get current user (auth required)
```

### Entries
```
GET    /api/entries         — List entries (search, mood, favorite, pagination)
GET    /api/entries/stats   — User stats (count, streak, words, moods)
GET    /api/entries/calendar — Entries by month
GET    /api/entries/:id     — Single entry with tags & images
POST   /api/entries         — Create entry
PUT    /api/entries/:id     — Update entry
DELETE /api/entries/:id     — Delete entry
```

### Profile
```
GET    /api/profile         — Get profile + stats
PUT    /api/profile         — Update display_name, bio, username
PUT    /api/profile/password — Change password
POST   /api/profile/avatar  — Upload profile image
POST   /api/profile/upload-image — Upload journal image
```

### Settings
```
GET    /api/settings        — Get user settings
PUT    /api/settings        — Update settings
GET    /api/settings/themes — List available themes
```

---

## ✦ Design System

### Colors
```
--cream:         #F5F0E8   (main background)
--cream-light:   #FAF7F2   (paper/card background)
--parchment:     #E8E0D0   (borders, subtle bg)
--bark:          #8B7355   (warm brown accent)
--bark-light:    #C4A882   (lighter accent)
--ink:           #2C2420   (primary text)
--ink-light:     #5C4F44   (secondary text)
--ink-muted:     #9A8B7E   (muted/label text)
```

### Fonts
- **Playfair Display** — Large headings, logo
- **Cormorant Garamond** — Body text, journal writing
- **Caveat** — Handwritten labels, sticky notes
- **DM Sans** — UI elements, labels, navigation

### Special Effects
- 🟫 Paper grain texture (SVG filter overlay)
- 📌 Tape strips (CSS with diagonal texture)
- 📸 Polaroid frames (white padding + caption)
- 📒 Dotted / lined / grid paper modes
- 🌿 Floating botanical decorations
- ✨ Framer Motion fade-ups and hover elevations

---

## ✦ Features

- ✅ JWT authentication with persistent sessions
- ✅ bcrypt password hashing
- ✅ Create, edit, delete journal entries
- ✅ Rich mood tagging (8 moods)
- ✅ Custom tags with inline editor
- ✅ Image uploads (polaroid display)
- ✅ Auto-save (4-second debounce)
- ✅ Draft / Published toggle
- ✅ Favorites
- ✅ Paper mode: dotted / lined / grid / plain
- ✅ Monthly calendar with mood indicators
- ✅ Dashboard with stats + mini calendar
- ✅ Profile with memory gallery
- ✅ 5 aesthetic themes
- ✅ Search & filter entries
- ✅ Responsive design
- ✅ Smooth Framer Motion animations

---

## ✦ Notes

- Images are stored locally in `backend/uploads/`
- JWT tokens expire after 7 days
- Auto-save triggers 4 seconds after any change
- The `uploads` folder must exist before running the server

---

*"Write what should not be forgotten. Keep what matters. Let go of what doesn't."*
