# 🚀 Vercel Deployment Guide for EZ-NOTI

## Prerequisites
1. **Vercel Account**: Sign up at [vercel.com](https://vercel.com)
2. **Vercel CLI**: Install globally with `npm i -g vercel`
3. **Firebase Service Account**: Your Firebase service account key JSON

## 🛠️ Deployment Steps

### 1. Install Vercel CLI
```bash
npm install -g vercel
```

### 2. Login to Vercel
```bash
vercel login
```

### 3. Set Environment Variables
You need to set these environment variables in Vercel:

#### Required Variables:
- `FIREBASE_SERVICE_ACCOUNT_JSON`: Your entire Firebase service account JSON as a string
- `FIREBASE_DATABASE_URL`: Your Firebase Realtime Database URL (optional)
- `NODE_ENV`: Set to `production`

#### How to set environment variables:
1. Go to your Vercel dashboard
2. Select your project
3. Go to Settings → Environment Variables
4. Add the variables above

### 4. Deploy to Vercel
From your project root directory:
```bash
vercel
```

Or for production deployment:
```bash
vercel --prod
```

## 🔧 Environment Variables Setup

### FIREBASE_SERVICE_ACCOUNT_JSON
This should be your entire Firebase service account JSON file content as a single string. 

**Example:**
```json
{"type":"service_account","project_id":"your-project-id","private_key_id":"...","private_key":"-----BEGIN PRIVATE KEY-----\n...\n-----END PRIVATE KEY-----\n","client_email":"...","client_id":"...","auth_uri":"...","token_uri":"...","auth_provider_x509_cert_url":"...","client_x509_cert_url":"..."}
```

### FIREBASE_DATABASE_URL (Optional)
If you're using Firebase Realtime Database:
```
https://your-project-id-default-rtdb.firebaseio.com/
```

## 📁 Project Structure After Setup
```
EZ-NOTI/
├── vercel.json              # Vercel configuration
├── package.json             # Root package.json for Vercel
├── .vercelignore           # Files to ignore during deployment
├── server/
│   ├── server.js           # Modified for serverless
│   ├── package.json        # Server dependencies
│   └── public/            # Static files
└── firebase-setup/         # Excluded from deployment
```

## 🌐 After Deployment

1. **Test Your Deployment**: Visit your Vercel URL
2. **Health Check**: Visit `https://your-app.vercel.app/health`
3. **Firebase Info**: Visit `https://your-app.vercel.app/api/firebase-info`
4. **Web Interface**: Visit `https://your-app.vercel.app/`

## 🔍 Troubleshooting

### Common Issues:

1. **Firebase Not Initialized**
   - Check that `FIREBASE_SERVICE_ACCOUNT_JSON` is properly set
   - Ensure the JSON is valid and properly escaped

2. **Static Files Not Loading**
   - Verify `server/public/` directory structure
   - Check vercel.json routes configuration

3. **API Routes Not Working**
   - Ensure all API routes start with `/api/`
   - Check function timeout settings in vercel.json

### Debug Commands:
```bash
# Check deployment logs
vercel logs

# Check environment variables
vercel env ls

# Remove deployment
vercel remove
```

## 🔄 Updating Deployment

To update your deployment:
```bash
# From project root
vercel --prod
```

## 📝 Notes

- The server runs in serverless mode on Vercel
- Static files are served from `/server/public/`
- Environment variables are loaded automatically
- Firebase is initialized on first request (cold start)
- Keep your Firebase service account secure - never commit it to git

## 🎯 Quick Deploy Commands

```bash
# One-time setup
npm install -g vercel
vercel login

# Deploy
cd /path/to/EZ-NOTI
vercel --prod
```

Your app will be available at: `https://your-project-name.vercel.app`
