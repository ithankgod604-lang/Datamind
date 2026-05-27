# 🚀 DataMind AI - Complete Setup & Troubleshooting Guide

## Table of Contents
1. [Local Development Setup](#local-development-setup)
2. [Netlify Deployment](#netlify-deployment)
3. [Environment Variables](#environment-variables)
4. [Testing & Verification](#testing--verification)
5. [Troubleshooting](#troubleshooting)
6. [FAQ](#faq)

---

## Local Development Setup

### Step 1: Prerequisites Check
```bash
# Check Node.js version (need 18 or higher)
node --version

# Check npm version
npm --version
```

**Required**: Node.js 18.x or higher  
**Get it**: [nodejs.org](https://nodejs.org/)

### Step 2: Clone Repository
```bash
git clone https://github.com/ithankgod604-lang/Datamind.git
cd Datamind
```

### Step 3: Install Dependencies
```bash
npm install
```

### Step 4: Get Anthropic API Key

1. Visit: https://console.anthropic.com/account/keys
2. Log in with your Anthropic account (create one if needed)
3. Click "Create Key"
4. Copy the key (you won't see it again!)

### Step 5: Create .env File
```bash
cp .env.example .env
# Edit with your API key
```

Add your API key:
```
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxxxxxxxxx
```

### Step 6: Start Development Server
```bash
npm run dev
```

### Step 7: Open in Browser
- Visit: **http://localhost:8888**

---

## Netlify Deployment

### Option A: Automatic Deployment (Recommended)

#### Step 1: Push to GitHub
```bash
git add .
git commit -m "Fix: Restore Netlify functions and dependencies"
git push origin fix/restore-netlify-functions
```

#### Step 2: Connect to Netlify
1. Go to: https://app.netlify.com
2. Click "New site from Git"
3. Select repository: `ithankgod604-lang/Datamind`
4. Click "Deploy site"

#### Step 3: Set Environment Variables
1. **Site Settings → Environment → Variables**
2. Add `ANTHROPIC_API_KEY=sk-ant-...`
3. Save

#### Step 4: Trigger Deployment
1. Go to **Deployments** tab
2. Click "Trigger deploy"

Your site will be live at: **https://your-site-name.netlify.app**

### Option B: Manual Deployment with Netlify CLI

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy to production
netlify deploy --prod

# Set environment variable
netlify env:set ANTHROPIC_API_KEY sk-ant-xxxxxxxxxxxxxxxxxxxx
```

---

## Environment Variables

### Netlify Dashboard Method

1. **Site Settings → Environment → Variables**
2. Click "Add variable"
3. Add `ANTHROPIC_API_KEY=sk-ant-...`
4. Save and redeploy

### Using Netlify CLI

```bash
# Set variable
netlify env:set ANTHROPIC_API_KEY sk-ant-...

# List variables
netlify env:list
```

---

## Testing & Verification

### Test Locally

#### 1. Upload a Dataset
- Open http://localhost:8888
- Click "Upload Dataset"
- Select a CSV file
- Verify file uploads successfully

#### 2. Test Phase Analysis
- Click "Phase 1 Understand"
- Enter a task
- Click "Analyze"
- Verify AI response appears

#### 3. Test AI Tools
- Click "SQL Engine"
- Ask a question
- Verify SQL query is generated

#### 4. Check Browser Console
- Press `F12`
- Look for error messages
- No red errors = good!

### Test on Netlify

#### 1. Check Deployment Status
- Netlify Dashboard → **Deployments**
- Latest deployment should show **Published**

#### 2. Check Function Logs
- Netlify Dashboard → **Functions**
- Click `claude` function
- Look for any errors

#### 3. Load Website
- Open your deployed site
- Try uploading a file
- Test AI features
- Check browser console (F12)

---

## Troubleshooting

### Problem: "Cannot reach AI. Check internet and Netlify deployment."

**Solution:**
```bash
# 1. Verify API key format (should start with sk-ant-)
cat .env

# 2. Set/update environment variable on Netlify
netlify env:set ANTHROPIC_API_KEY sk-ant-your-actual-key

# 3. Redeploy
netlify deploy --prod

# 4. Wait 2-3 minutes for propagation
# 5. Test again
```

### Problem: "claude.js not found" or "404 error"

**Solution:**
```bash
# Verify file exists
ls -la netlify/functions/

# If missing, git pull latest
git pull origin fix/restore-netlify-functions

# Reinstall
npm install

# Redeploy
netlify deploy --prod
```

### Problem: "CORS error" in browser console

**Solution:**
```bash
# Verify netlify.toml has CORS headers
cat netlify.toml | grep -A 5 "Access-Control"

# If missing, pull latest:
git pull origin fix/restore-netlify-functions

# Redeploy:
netlify deploy --prod
```

### Problem: File upload fails or hangs

**Solution:**
```
Netlify limit: 50MB per file

If file is larger:
1. Use Excel/CSV tools to split file
2. Upload in chunks
3. Contact Netlify support for limits
```

### Problem: "npm ERR! Cannot find module"

**Solution:**
```bash
# Clear cache
npm cache clean --force

# Reinstall
rm -rf node_modules
npm install

# Verify
npm list
```

---

## FAQ

### Q: Where do I get my Anthropic API key?
**A**: https://console.anthropic.com/account/keys (requires free Anthropic account)

### Q: Is my API key safe?
**A**: Yes! Netlify keeps environment variables secure. Never commit `.env` file to GitHub.

### Q: How much does Claude API cost?
**A**: Per-token pricing. Check: https://www.anthropic.com/pricing

### Q: Why does it take 5-10 seconds for AI responses?
**A**: Network latency + AI processing time. This is normal.

### Q: Can I run this offline?
**A**: No, it requires Anthropic API connection.

### Q: What happens if my API key expires?
**A**: Generate a new key and update Netlify environment variables.

### Q: Can multiple people use the same deployment?
**A**: Yes! Unlimited concurrent users.

### Q: How do I monitor API usage?
**A**: Check Anthropic console: https://console.anthropic.com/account/usage

### Q: How do I report bugs?
**A**: https://github.com/ithankgod604-lang/Datamind/issues

---

## Quick Checklist

- [ ] Node.js 18+ installed
- [ ] Repository cloned
- [ ] Dependencies installed (`npm install`)
- [ ] `.env` file created with API key
- [ ] `npm run dev` starts successfully
- [ ] Dashboard loads at http://localhost:8888
- [ ] File upload works
- [ ] AI features respond
- [ ] Deployed to Netlify
- [ ] Environment variable set on Netlify
- [ ] Site loads from netlify.app domain
- [ ] AI features work on live site

---

**All set! 🎉 Your DataMind AI instance is ready to use.**

For questions, visit: https://github.com/ithankgod604-lang/Datamind
