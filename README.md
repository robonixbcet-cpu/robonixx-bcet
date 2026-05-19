# 🤖 Robonixx — IoT & Robotics Club Website

A full-stack MERN web application for **Robonixx**, a college IoT & Robotics club. Features a futuristic deep-space UI, complete admin panel, event management, member directory, gallery, and contact system.

---

## ✨ Features

### 🌐 Public Frontend
- **Hero Section** — Animated particle background, tagline, motto, HOD display
- **Events** — Upcoming & past events with filtering, detailed pages, schedule timelines
- **Members** — Batch-wise directory with social links and search/filter
- **Gallery** — Masonry grid with lightbox preview
- **About** — Mission, values, core team showcase
- **Contact** — Form with Nodemailer, embedded Google Maps

### 🔐 Admin Panel
- JWT-secured login
- **Dashboard** — Stats cards + Recharts analytics (bar chart, pie chart)
- **Events CRUD** — Create/edit/delete events with image upload (Cloudinary)
- **Members CRUD** — Batch-wise management, core team designation
- **Gallery Manager** — Multi-image upload + delete (Cloudinary)
- **Site Content Editor** — Edit tagline, motto, HOD info, social links
- **Messages Inbox** — View, mark read, reply, delete contact messages

---

## 🛠️ Tech Stack

| Layer | Tech |
|-------|------|
| Frontend | React 18, Vite, Tailwind CSS, Framer Motion |
| Backend | Node.js, Express.js |
| Database | MongoDB (Mongoose) |
| Auth | JWT (jsonwebtoken + bcryptjs) |
| File Uploads | Multer + Cloudinary |
| Email | Nodemailer (Gmail SMTP) |
| Charts | Recharts |
| Fonts | Orbitron, Syne, JetBrains Mono |

---

## 📁 Folder Structure

```
robonixx/
├── server/                     # Backend
│   ├── config/
│   │   └── cloudinary.js       # Cloudinary + Multer config
│   ├── middleware/
│   │   └── auth.js             # JWT protect + adminOnly
│   ├── models/
│   │   ├── User.js             # Admin user model
│   │   ├── Event.js            # Event model
│   │   ├── Member.js           # Member model
│   │   ├── SiteContent.js      # Site settings model
│   │   └── index.js            # Gallery + ContactMessage models
│   ├── routes/
│   │   ├── auth.js             # Login, /me, stats
│   │   ├── events.js           # Events CRUD
│   │   ├── members.js          # Members CRUD
│   │   ├── gallery.js          # Gallery CRUD
│   │   ├── contact.js          # Contact form + inbox
│   │   └── content.js          # Site content CRUD
│   ├── server.js               # Main entry point
│   ├── .env.example
│   └── package.json
│
├── client/                     # Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── admin/
│   │   │   │   └── AdminLayout.jsx     # Sidebar layout
│   │   │   ├── ui/
│   │   │   │   ├── PageLoader.jsx
│   │   │   │   ├── ParticleBackground.jsx
│   │   │   │   └── SectionHeader.jsx
│   │   │   ├── EventCard.jsx
│   │   │   ├── MemberCard.jsx
│   │   │   ├── Navbar.jsx
│   │   │   └── Footer.jsx
│   │   ├── context/
│   │   │   ├── AuthContext.jsx
│   │   │   └── ThemeContext.jsx
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── About.jsx
│   │   │   ├── Events.jsx
│   │   │   ├── EventDetail.jsx
│   │   │   ├── Gallery.jsx
│   │   │   ├── Members.jsx
│   │   │   ├── Contact.jsx
│   │   │   └── admin/
│   │   │       ├── AdminLogin.jsx
│   │   │       ├── AdminDashboard.jsx
│   │   │       ├── AdminEvents.jsx
│   │   │       ├── AdminMembers.jsx
│   │   │       ├── AdminGallery.jsx
│   │   │       ├── AdminContent.jsx
│   │   │       └── AdminMessages.jsx
│   │   ├── utils/
│   │   │   └── api.js          # Axios instance + API service methods
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css           # Tailwind + custom styles
│   ├── tailwind.config.js
│   ├── vite.config.js
│   ├── .env.example
│   └── package.json
│
├── package.json                # Root (concurrently dev scripts)
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js v18+
- MongoDB Atlas account (free tier)
- Cloudinary account (free tier)
- Gmail account (for Nodemailer)

---

### 1. Clone & Install

```bash
git clone https://github.com/yourusername/robonixx.git
cd robonixx
npm run install:all
```

### 2. Configure Environment Variables

**Backend** — `server/.env`:
```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb+srv://user:pass@cluster.mongodb.net/robonixx
JWT_SECRET=your_super_secret_key_change_this
JWT_EXPIRES_IN=7d

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_gmail_app_password
EMAIL_FROM=Robonixx Club <your_email@gmail.com>
ADMIN_EMAIL=admin@robonixx.com

CLIENT_URL=http://localhost:5173

# Seed admin (first run only)
ADMIN_NAME=Admin
ADMIN_EMAIL_SEED=username
ADMIN_PASSWORD_SEED=Your Password
```

**Frontend** — `client/.env`:
```env
VITE_API_URL=http://localhost:5000/api
```

### 3. Gmail App Password Setup
1. Go to Google Account → Security
2. Enable 2-Step Verification
3. Go to App Passwords → Generate password for "Mail"
4. Use that as `EMAIL_PASS`

### 4. Run Development

```bash
# Run both frontend and backend simultaneously
npm run dev

# Or separately:
npm run server    # Backend on http://localhost:5000
npm run client    # Frontend on http://localhost:5173
```

### 5. Access Admin Panel
Navigate to `http://localhost:5173/admin/login`  
Default credentials (from seed):
- **Email:** `admin@robonixx.com`  
- **Password:** `Robonixx@Admin123`

> ⚠️ Change the password after first login!

---

## 📡 API Reference

### Auth
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/api/auth/login` | Public | Admin login |
| GET | `/api/auth/me` | 🔐 | Get current admin |
| GET | `/api/auth/stats` | 🔐 Admin | Dashboard statistics |
| PUT | `/api/auth/change-password` | 🔐 | Change password |

### Events
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/api/events` | Public | List events (query: status, category, page, limit, featured) |
| GET | `/api/events/:idOrSlug` | Public | Get event by ID or slug |
| POST | `/api/events` | 🔐 Admin | Create event (multipart/form-data) |
| PUT | `/api/events/:id` | 🔐 Admin | Update event |
| DELETE | `/api/events/:id` | 🔐 Admin | Delete event + Cloudinary image |

### Members
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/api/members` | Public | List members (query: batch, isCore, search) |
| GET | `/api/members/batches` | Public | Get available batch list |
| GET | `/api/members/:id` | Public | Get member by ID |
| POST | `/api/members` | 🔐 Admin | Add member (multipart/form-data) |
| PUT | `/api/members/:id` | 🔐 Admin | Update member |
| DELETE | `/api/members/:id` | 🔐 Admin | Remove member |

### Gallery
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/api/gallery` | Public | Get images (query: category, page, limit) |
| POST | `/api/gallery` | 🔐 Admin | Upload images (up to 20, multipart/form-data) |
| PUT | `/api/gallery/:id` | 🔐 Admin | Update caption/category |
| DELETE | `/api/gallery/:id` | 🔐 Admin | Delete image |

### Contact
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| POST | `/api/contact` | Public | Submit contact form (rate limited: 5/hr) |
| GET | `/api/contact` | 🔐 Admin | Get messages (query: read, page, limit) |
| PUT | `/api/contact/:id/read` | 🔐 Admin | Mark as read |
| DELETE | `/api/contact/:id` | 🔐 Admin | Delete message |

---

## 🚢 Deployment

This repo is ready to deploy with:
- `client/` on Vercel
- `server/` on Render

### 1. Final Local Check Before Pushing

1. Make sure `.env` files are not committed.
2. Make sure your latest changes are committed locally.
3. Run a final frontend build:

```bash
cd client
npm run build
```

4. Push the repo to GitHub.
5. Keep these files in the repo:
   - `client/vercel.json`
   - `render.yaml`

### 2. Prepare Your Production Values

Before opening Vercel or Render, keep these values ready:

- MongoDB Atlas connection string
- Cloudinary cloud name, API key, API secret
- Gmail address for Nodemailer
- Gmail App Password
- production admin email and password
- final frontend URL
- optional custom domain

### 3. Deploy Backend on Render First

Deploy the backend first, because Vercel needs the backend URL in `VITE_API_URL`.

#### Option A: Use `render.yaml`

1. Open Render.
2. Click `New`.
3. Choose `Blueprint`.
4. Connect your GitHub repo.
5. Render will detect `render.yaml`.
6. Continue with the setup.

#### Option B: Create the service manually

1. Open Render.
2. Click `New`.
3. Choose `Web Service`.
4. Connect your GitHub repo.
5. Select this repository.
6. Use these settings:

```text
Name: robonixx-api
Root Directory: server
Environment: Node
Build Command: npm install
Start Command: node server.js
Health Check Path: /api/health
```

#### Render environment variables

Set these in the Render dashboard:

```env
NODE_ENV=production
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_long_random_secret
JWT_EXPIRES_IN=7d

CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=robonix.bcet@gmail.com
EMAIL_PASS=your_google_app_password
EMAIL_FROM=Robonixx Club <robonix.bcet@gmail.com>
ADMIN_EMAIL=robonix.bcet@gmail.com

CLIENT_URL=https://your-frontend.vercel.app
CLIENT_URLS=https://your-frontend.vercel.app,https://your-custom-domain.com

ADMIN_NAME=Admin
ADMIN_EMAIL_SEED=your_admin_login_email
ADMIN_PASSWORD_SEED=your_strong_admin_password
MAX_IMAGE_SIZE_MB=15
```

Important:
- `CLIENT_URL` can be temporary at first.
- If you do not yet know the Vercel URL, set it later and redeploy.
- `ADMIN_EMAIL` is for contact form email notifications.
- `ADMIN_EMAIL_SEED` is for the admin login account seeding logic.

#### First Render deploy check

After deployment finishes:

1. Open your backend URL, for example:

```text
https://your-backend-name.onrender.com/api/health
```

2. Confirm it returns a success JSON response.
3. If it fails, check Render logs first.

### 4. Deploy Frontend on Vercel

Once Render gives you the backend URL, deploy the frontend.

1. Open Vercel.
2. Click `Add New...`
3. Choose `Project`.
4. Import the same GitHub repo.
5. Set the **Root Directory** to:

```text
client
```

6. Confirm the build settings:

```text
Framework Preset: Vite
Build Command: npm run build
Output Directory: dist
Install Command: npm install
```

7. Add this environment variable before deploying:

```env
VITE_API_URL=https://your-backend-name.onrender.com/api
```

8. Click `Deploy`.

The included `client/vercel.json` already handles SPA route rewrites, so URLs like `/admin/login`, `/gallery`, and `/events/...` should work on refresh.

### 5. Update Render CORS With the Real Vercel URL

After Vercel finishes, it gives you a production URL like:

```text
https://your-project.vercel.app
```

Now go back to Render and update:

```env
CLIENT_URL=https://your-project.vercel.app
CLIENT_URLS=https://your-project.vercel.app,https://your-custom-domain.com
```

Then redeploy the Render backend.

If you are not using a custom domain yet, `CLIENT_URLS` can be just the Vercel URL:

```env
CLIENT_URLS=https://your-project.vercel.app
```

### 6. Test the Deployed Site Step by Step

After both deployments are live:

1. Open the frontend homepage on Vercel.
2. Open browser dev tools and confirm public API calls succeed.
3. Visit `/admin/login`.
4. Log in with your admin account.
5. Test events CRUD.
6. Test members CRUD.
7. Test gallery upload.
8. Test contact form submission.
9. Open the admin messages panel and confirm the message is saved.
10. Check `robonix.bcet@gmail.com` for the email notification.
11. Check that gallery images and videos load correctly.
12. Refresh pages like `/gallery` and `/admin/login` directly to confirm Vercel rewrites work.

### 7. Optional Custom Domain Setup

If you want your own domain:

1. Add the custom domain in Vercel for the frontend.
2. Add DNS records as Vercel instructs.
3. If needed, also add a backend custom domain in Render.
4. Update these env vars:

```env
VITE_API_URL=https://api.yourdomain.com/api
CLIENT_URL=https://www.yourdomain.com
CLIENT_URLS=https://www.yourdomain.com,https://yourdomain.com
```

5. Redeploy both services after changing production env vars.

### 8. Production Checklist

- Backend `/api/health` works
- Frontend loads from Vercel
- CORS is not blocking requests
- Admin login works
- Contact form saves messages
- Nodemailer sends email
- Cloudinary uploads work
- Gallery media renders correctly
- Refresh on nested frontend routes works
- Custom domain works if configured

### 9. Notes

- Render free web services can spin down when idle, so the first request after inactivity may be slow.
- Render uses an ephemeral filesystem, which is fine here because uploads are stored in Cloudinary and data is stored in MongoDB.
- Vercel must use `VITE_API_URL` that points to the deployed backend.
- If you change any env var on Vercel or Render, redeploy that service.

### Site Content
| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/api/content/:key` | Public | Get content by key |
| PUT | `/api/content/:key` | 🔐 Admin | Update content |
| POST | `/api/content/upload/image` | 🔐 Admin | Upload HOD/content image |

### Database → MongoDB Atlas
1. Create a free cluster
2. Whitelist `0.0.0.0/0` for Render
3. Copy connection string to `MONGO_URI`

---

## 🎨 UI Theme Reference

| Token | Value | Usage |
|-------|-------|-------|
| `space-900` | `#0B0F1A` | Main background |
| `space-800` | `#111827` | Card backgrounds |
| `space-700` | `#1F2A44` | Borders, inputs |
| `primary` | `#5DADE2` | Main accent (blue) |
| `accent` | `#A29BFE` | Secondary accent (violet) |

**Fonts:**
- `font-display` — Orbitron (headings, logos)
- `font-body` — Syne (body text)
- `font-mono` — JetBrains Mono (code, tags, badges)

---

## 📝 License
MIT — Built with ❤️ for Robonixx Club
# Robonixx-Website
