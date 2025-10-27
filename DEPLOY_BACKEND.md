# 🚀 Backend Deployment Guide

## Quick Deploy Backend (3 Minutes)

Your frontend is already deployed to GitHub Pages. Now deploy the backend!

---

## Option 1: Deploy to Render (Recommended - Easiest)

### Step 1: Sign Up for Render

1. Go to: https://render.com
2. Click "Get Started for Free"
3. Sign up with GitHub

### Step 2: Create New Web Service

1. Click "New +" → "Web Service"
2. Connect your GitHub account (if not already connected)
3. Select repository: `prakashorton/pdf-form-reader`
4. Click "Connect"

### Step 3: Configure Service

**Basic Settings:**
- **Name**: `pdf-form-reader-backend`
- **Region**: Oregon (US West) or closest to you
- **Branch**: `main`
- **Root Directory**: `pdf-form-reader/server`
- **Runtime**: Node
- **Build Command**: `npm install`
- **Start Command**: `node index.js`

**Environment Variables:**
- Click "Advanced" → "Add Environment Variable"
- Key: `PORT` → Value: `3001`
- Key: `NODE_ENV` → Value: `production`

**Instance Type:**
- Select: **Free** (0.1 CPU, 512 MB RAM)

### Step 4: Deploy

1. Click "Create Web Service"
2. Wait 2-3 minutes for deployment
3. Copy your backend URL (e.g., `https://pdf-form-reader-backend.onrender.com`)

### Step 5: Update Frontend

Edit `pdf-form-reader/src/App.tsx`:

```typescript
// Change this line:
const API_URL = 'http://localhost:3001';

// To this (replace with your Render URL):
const API_URL = 'https://pdf-form-reader-backend.onrender.com';
```

### Step 6: Commit and Push

```bash
git add .
git commit -m "Update API URL to Render backend"
git push origin main
```

GitHub Pages will automatically redeploy your frontend!

---

## Option 2: Deploy to Railway

### Step 1: Sign Up for Railway

1. Go to: https://railway.app
2. Sign in with GitHub

### Step 2: Create New Project

1. Click "New Project"
2. Select "Deploy from GitHub repo"
3. Choose `prakashorton/pdf-form-reader`
4. Railway will detect the repository

### Step 3: Configure Service

1. Click "Add variables"
2. Add: `PORT=3001`
3. Click "Settings"
4. Set "Root Directory": `pdf-form-reader/server`
5. Set "Start Command": `node index.js`

### Step 4: Deploy

1. Railway will automatically deploy
2. Click "Generate Domain" to get your URL
3. Copy the URL (e.g., `https://pdf-form-reader-production.up.railway.app`)

### Step 5: Update Frontend

Same as Option 1, Step 5 - update `API_URL` in `App.tsx`

---

## Option 3: Deploy to Heroku

### Step 1: Install Heroku CLI

```bash
npm install -g heroku
```

### Step 2: Login to Heroku

```bash
heroku login
```

### Step 3: Create Heroku App

```bash
heroku create pdf-form-reader-backend
```

### Step 4: Add Buildpack

```bash
heroku buildpacks:set heroku/nodejs
```

### Step 5: Set Root Directory

Create `Procfile` in root:
```
web: cd pdf-form-reader/server && npm install && node index.js
```

### Step 6: Deploy

```bash
git push heroku main
```

### Step 7: Update Frontend

Same as Option 1, Step 5 - update `API_URL` in `App.tsx`

---

## Verify Backend Deployment

After deploying, test your backend:

### Test Health Check

```bash
curl https://your-backend-url.com/
```

Expected response:
```json
{
  "status": "ok",
  "message": "PDF Form Reader API is running",
  "endpoints": {
    "health": "/api/health",
    "extract": "/api/extract-pdf-fields"
  }
}
```

### Test in Browser

Open: `https://your-backend-url.com/`

You should see the JSON response above.

---

## Update Frontend After Backend Deployment

### 1. Update API URL

Edit `pdf-form-reader/src/App.tsx`:

```typescript
const API_URL = import.meta.env.VITE_API_URL || 'https://your-backend-url.com';
```

### 2. Add Environment Variable (Optional)

Create `pdf-form-reader/.env.production`:

```env
VITE_API_URL=https://your-backend-url.com
```

### 3. Commit and Push

```bash
git add .
git commit -m "Connect frontend to deployed backend"
git push origin main
```

---

## Troubleshooting

### CORS Errors

If you see CORS errors in browser console:

1. Check `pdf-form-reader/server/index.js` has your GitHub Pages URL:
   ```javascript
   app.use(cors({
     origin: [
       'http://localhost:5173',
       'https://prakashorton.github.io'
     ]
   }));
   ```

2. Commit and push to redeploy backend

### Backend Not Starting

**Check logs:**
- **Render**: Dashboard → Your Service → Logs
- **Railway**: Dashboard → Your Service → Deployments → View Logs
- **Heroku**: `heroku logs --tail`

**Common issues:**
- Missing `package.json` in server directory
- Wrong start command
- Port configuration (should use `process.env.PORT`)

### 404 Errors

Make sure:
- Root directory is set to `pdf-form-reader/server`
- Start command is `node index.js`
- All dependencies are in `package.json`

---

## Cost Comparison

| Platform | Free Tier | Limitations |
|----------|-----------|-------------|
| **Render** | ✅ Yes | Spins down after 15 min inactivity |
| **Railway** | ✅ $5/month credit | ~500 hours/month |
| **Heroku** | ✅ Yes | Sleeps after 30 min inactivity |

**Recommendation**: Use **Render** for easiest setup with generous free tier.

---

## Final Architecture

```
┌─────────────────────────────────────┐
│   GitHub Pages (Frontend)           │
│   https://prakashorton.github.io/   │
│   pdf-form-reader/                  │
└──────────────┬──────────────────────┘
               │
               │ API Calls
               │
               ▼
┌─────────────────────────────────────┐
│   Render/Railway (Backend)          │
│   https://your-backend.com          │
│   Node.js + Express                 │
└─────────────────────────────────────┘
```

---

## Next Steps

1. ✅ Choose deployment platform (Render recommended)
2. ✅ Deploy backend (3 minutes)
3. ✅ Copy backend URL
4. ✅ Update frontend API_URL
5. ✅ Commit and push
6. ✅ Test full application!

---

**Ready to deploy? Start with Option 1 (Render) - it's the easiest!** 🚀

