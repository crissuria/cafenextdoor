# Quick Deployment Guide - Cafe Next Door

## 🚀 Easiest Option: Render.com (Recommended)

### Step 1: Prepare Your Code
✅ Your app is already prepared with:
- ✅ `Procfile` (for Render/Heroku)
- ✅ `wsgi.py` (WSGI entry point)
- ✅ `requirements.txt` (with gunicorn)
- ✅ `runtime.txt` (Python version)

### Step 2: Push to GitHub (if not already done)

1. **Initialize Git** (if not already):
   ```bash
   git init
   git add .
   git commit -m "Ready for deployment"
   ```

2. **Create GitHub Repository**:
   - Go to https://github.com/new
   - Create a new repository (e.g., "cafe-next-door")
   - **DO NOT** initialize with README

3. **Push to GitHub**:
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/cafe-next-door.git
   git branch -M main
   git push -u origin main
   ```

### Step 3: Deploy on Render

1. **Sign up/Login** at https://render.com (free account)

2. **Create New Web Service**:
   - Click "New +" → "Web Service"
   - Connect your GitHub repository
   - Select your `cafe-next-door` repository

3. **Configure Settings**:
   - **Name**: `cafe-next-door` (or your preferred name)
   - **Region**: Choose closest to your users
   - **Branch**: `main`
   - **Root Directory**: (leave empty)
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn wsgi:application`

4. **Add Environment Variables**:
   Click "Advanced" → "Add Environment Variable" and add:
   
   ```
   SECRET_KEY=your-generated-secret-key-here
   FLASK_ENV=production
   FLASK_DEBUG=False
   ```
   
   **Generate Secret Key**:
   ```bash
   python -c "import secrets; print(secrets.token_hex(32))"
   ```
   
   Copy the output and use it as `SECRET_KEY`

5. **Optional Environment Variables** (for email):
   ```
   MAIL_SERVER=smtp.gmail.com
   MAIL_PORT=587
   MAIL_USE_TLS=True
   MAIL_USERNAME=your-email@gmail.com
   MAIL_PASSWORD=your-app-password
   MAIL_DEFAULT_SENDER=your-email@gmail.com
   CAFE_EMAIL=your-cafe-email@gmail.com
   ```

6. **Deploy!**
   - Click "Create Web Service"
   - Render will build and deploy automatically
   - Wait 2-5 minutes for first deployment

7. **Your App URL**:
   - Render provides: `https://cafe-next-door.onrender.com` (or your custom name)
   - Free tier: App spins down after 15 min inactivity (wakes up on first request)

### Step 4: After Deployment

1. **Visit your app URL**
2. **Login as admin**:
   - Username: `admin`
   - Password: `admin123`
   - **CHANGE THIS PASSWORD IMMEDIATELY!**

3. **Initialize Database** (if needed):
   - The database should auto-initialize, but if you see errors:
   - Go to admin dashboard → Database should initialize on first use

---

## 🚂 Alternative: Railway.app (Also Easy)

1. **Sign up** at https://railway.app
2. **New Project** → "Deploy from GitHub repo"
3. **Select your repository**
4. **Railway auto-detects Flask** - no configuration needed!
5. **Add Environment Variables** (same as Render)
6. **Deploy!**

Railway provides: `https://your-app-name.up.railway.app`

---

## 📋 Pre-Deployment Checklist

Before deploying, make sure:

- [ ] All code is committed to Git
- [ ] `.env` file is in `.gitignore` (✅ already done)
- [ ] `SECRET_KEY` is generated and ready
- [ ] Test app locally first
- [ ] Database folder exists (will be created automatically)

---

## 🔧 Troubleshooting

### App shows 500 error:
1. Check Render logs (in dashboard)
2. Verify environment variables are set
3. Check that `SECRET_KEY` is set

### Database errors:
- Database will auto-create on first use
- If issues persist, check Render logs

### Static files not loading:
- Verify `static/` folder is in repository
- Check file paths are correct

---

## 💡 Tips

- **Free Tier Limits**:
  - Render: Spins down after 15 min inactivity
  - Railway: 500 hours/month free
  
- **Custom Domain**:
  - Both platforms support custom domains
  - Add in platform settings after deployment

- **Database**:
  - SQLite works fine for small-medium apps
  - For larger scale, consider PostgreSQL (available on both platforms)

---

## 🎯 Quick Start Commands

```bash
# Generate Secret Key
python -c "import secrets; print(secrets.token_hex(32))"

# Test locally before deploying
python app.py
```

---

**Need help?** Check the deployment logs in your platform's dashboard!
