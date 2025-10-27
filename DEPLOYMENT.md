# 🚀 Deployment Guide

## Quick Deploy (5 Minutes)

### Prerequisites
- GitHub account
- Vercel account (free) - https://vercel.com
- Railway account (free) - https://railway.app

---

## Step 1: Push to GitHub

### Create GitHub Repository

1. **Go to GitHub**: https://github.com/new

2. **Create repository:**
   - Repository name: `pdf-form-reader`
   - Description: `PDF Form Reader with field extraction`
   - Public or Private: Your choice
   - **Don't** initialize with README (we already have one)

3. **Copy the repository URL**
   - Example: `https://github.com/yourusername/pdf-form-reader.git`

### Push Code to GitHub

```bash
# Add remote
git remote add origin https://github.com/yourusername/pdf-form-reader.git

# Push code
git branch -M main
git push -u origin main
```

---

## Step 2: Deploy Backend to Railway

### Setup Railway

1. **Go to Railway**: https://railway.app

2. **Sign in** with GitHub

3. **Create New Project**
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Choose your `pdf-form-reader` repository
   - Select `pdf-form-reader/server` as the root directory

4. **Configure Environment Variables**
   - Click on your service
   - Go to "Variables" tab
   - Add:
     ```
     PORT=3001
     ```

5. **Deploy**
   - Railway will automatically deploy
   - Wait for deployment to complete
   - Copy the deployment URL (e.g., `https://your-app.railway.app`)

### Get Backend URL

After deployment, Railway will give you a URL like:
```
https://pdf-form-reader-production.up.railway.app
```

**Save this URL - you'll need it for frontend!**

---

## Step 3: Deploy Frontend to Vercel

### Setup Vercel

1. **Go to Vercel**: https://vercel.com

2. **Sign in** with GitHub

3. **Import Project**
   - Click "Add New..." → "Project"
   - Import your `pdf-form-reader` repository
   - Select `pdf-form-reader` as the root directory

4. **Configure Build Settings**
   - Framework Preset: Vite
   - Root Directory: `pdf-form-reader`
   - Build Command: `npm run build`
   - Output Directory: `dist`

5. **Add Environment Variable**
   - Click "Environment Variables"
   - Add:
     ```
     VITE_API_URL=https://your-backend-url.railway.app
     ```
   - Replace with your actual Railway backend URL

6. **Deploy**
   - Click "Deploy"
   - Wait for deployment to complete
   - Vercel will give you a URL like: `https://pdf-form-reader.vercel.app`

---

## Step 4: Update Frontend API URL

After getting your Railway backend URL, update the frontend:

1. **Edit `pdf-form-reader/src/App.tsx`**
   
   Find this line:
   ```typescript
   const API_URL = 'http://localhost:3001';
   ```
   
   Replace with:
   ```typescript
   const API_URL = import.meta.env.VITE_API_URL || 'https://your-backend-url.railway.app';
   ```

2. **Commit and push**
   ```bash
   git add .
   git commit -m "Update API URL for production"
   git push
   ```

3. **Vercel will auto-deploy** the changes

---

## Step 5: Update Backend CORS

Update `pdf-form-reader/server/index.js` to allow your Vercel domain:

```javascript
app.use(cors({
  origin: [
    'http://localhost:5173',
    'https://pdf-form-reader.vercel.app',  // Add your Vercel URL
    'https://*.vercel.app'  // Allow all Vercel preview deployments
  ]
}));
```

Commit and push:
```bash
git add .
git commit -m "Update CORS for production"
git push
```

Railway will auto-deploy the changes.

---

## ✅ Deployment Complete!

Your application is now live:

- **Frontend**: https://pdf-form-reader.vercel.app
- **Backend**: https://your-backend-url.railway.app

---

## 🔧 Troubleshooting

### Frontend can't connect to backend

**Check:**
1. Backend is deployed and running on Railway
2. VITE_API_URL environment variable is set in Vercel
3. CORS is configured correctly in backend

**Fix:**
- Redeploy frontend with correct API URL
- Check Railway logs for errors

### Backend errors

**Check Railway logs:**
1. Go to Railway dashboard
2. Click on your service
3. Go to "Deployments" tab
4. Click on latest deployment
5. View logs

**Common issues:**
- Missing environment variables
- Port configuration (should be 3001)
- Node.js version mismatch

### CORS errors

**Fix:**
Add your Vercel domain to CORS whitelist in `server/index.js`:
```javascript
app.use(cors({
  origin: ['https://your-app.vercel.app']
}));
```

---

## 🔄 Continuous Deployment

Both Vercel and Railway support automatic deployments:

- **Push to GitHub** → Automatic deployment
- **Pull Request** → Preview deployment
- **Merge to main** → Production deployment

---

## 💰 Cost

Both platforms offer generous free tiers:

### Vercel (Frontend)
- ✅ Free for personal projects
- ✅ Unlimited deployments
- ✅ Automatic HTTPS
- ✅ Global CDN

### Railway (Backend)
- ✅ $5 free credit per month
- ✅ ~500 hours of runtime
- ✅ Automatic HTTPS
- ✅ Auto-scaling

---

## 🎯 Alternative Deployment Options

### Option 1: Netlify (Frontend) + Render (Backend)

**Netlify:**
- Similar to Vercel
- Free tier available
- https://netlify.com

**Render:**
- Similar to Railway
- Free tier available
- https://render.com

### Option 2: Heroku (All-in-one)

**Heroku:**
- Deploy both frontend and backend
- Free tier (with limitations)
- https://heroku.com

### Option 3: AWS/GCP/Azure

**Cloud Platforms:**
- More complex setup
- More control
- Pay-as-you-go pricing

---

## 📝 Post-Deployment Checklist

- [ ] Frontend deployed to Vercel
- [ ] Backend deployed to Railway
- [ ] Environment variables configured
- [ ] CORS configured correctly
- [ ] API URL updated in frontend
- [ ] Test PDF upload functionality
- [ ] Test field extraction
- [ ] Test interaction sync
- [ ] Check browser console for errors
- [ ] Check Railway logs for backend errors

---

## 🔐 Security Notes

1. **Never commit `.env` files** - Already in .gitignore
2. **Use environment variables** for sensitive data
3. **Enable HTTPS** - Automatic on Vercel/Railway
4. **Limit CORS origins** - Only allow your domains
5. **Rate limiting** - Consider adding for production

---

## 📚 Resources

- **Vercel Docs**: https://vercel.com/docs
- **Railway Docs**: https://docs.railway.app
- **Vite Deployment**: https://vitejs.dev/guide/static-deploy.html
- **Express Production**: https://expressjs.com/en/advanced/best-practice-performance.html

---

**Need help? Check the logs and error messages!**

