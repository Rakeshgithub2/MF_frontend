# Frontend Deployment to Vercel

## Environment Configuration

The frontend has been configured to use your deployed backend:
```
Backend URL: https://mf-backend-bd96.vercel.app
```

## Deployment Steps

### Option 1: Automatic Deployment (Recommended)

1. **Push to GitHub:**
   ```bash
   cd "c:\mutual fund\mutual-funds-portal"
   git add -A
   git commit -m "Configure production backend URL"
   git push origin master
   ```

2. **Import to Vercel:**
   - Go to https://vercel.com/new
   - Click **Import Git Repository**
   - Select: `Rakeshgithub2/MF_frontend`
   - Click **Import**

3. **Configure Environment Variables:**
   In Vercel Dashboard → Settings → Environment Variables, add:
   ```
   NEXT_PUBLIC_API_URL=https://mf-backend-bd96.vercel.app/api
   NODE_ENV=production
   ```

4. **Deploy:**
   - Click **Deploy**
   - Wait for build to complete
   - Get your frontend URL: `https://mf-frontend-xxx.vercel.app`

### Option 2: Manual Deployment

```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Deploy
cd "c:\mutual fund\mutual-funds-portal"
vercel --prod
```

## Post-Deployment Steps

### 1. Update Backend CORS

After getting your frontend URL, update backend environment variables in Vercel:

```
FRONTEND_URL=https://your-frontend-url.vercel.app
GOOGLE_REDIRECT_URI=https://mf-backend-bd96.vercel.app/api/auth/google/callback
```

### 2. Update Google OAuth Console

1. Go to https://console.cloud.google.com/
2. APIs & Services → Credentials
3. Edit your OAuth 2.0 Client ID
4. Add Authorized JavaScript origins:
   ```
   https://your-frontend-url.vercel.app
   ```
5. Add Authorized redirect URIs:
   ```
   https://mf-backend-bd96.vercel.app/api/auth/google/callback
   ```

## Environment Files

- `.env.local` → Local development (uses localhost:3002)
- `.env.production` → Production deployment (uses Vercel backend)
- `.env.example` → Template with production URL

## Files Updated

✅ All hardcoded `localhost:3002` URLs now use environment variables
✅ `.env.production` created with Vercel backend URL
✅ Calculator endpoints use dynamic API URL
✅ Market data endpoints use dynamic API URL
✅ Socket connection uses dynamic URL

## Testing After Deployment

1. **Test API Connection:**
   ```
   https://your-frontend.vercel.app
   ```

2. **Check Console for Errors:**
   - Open browser DevTools → Console
   - Look for CORS errors or API errors

3. **Test Key Features:**
   - ✓ Fund list loads
   - ✓ Portfolio page works
   - ✓ Calculators work
   - ✓ Google login works

## Troubleshooting

### CORS Errors
- Add your frontend URL to backend `FRONTEND_URL` variable
- Redeploy backend after updating

### API Not Found (404)
- Check `NEXT_PUBLIC_API_URL` is set correctly
- Verify backend is deployed and working

### Google OAuth Fails
- Update Google Console with new URLs
- Check `GOOGLE_REDIRECT_URI` in backend matches exactly

## Success Checklist

- [ ] Frontend deployed to Vercel
- [ ] Backend URL updated in frontend `.env.production`
- [ ] Frontend URL updated in backend `FRONTEND_URL`
- [ ] Google OAuth URLs updated in console
- [ ] CORS configured correctly
- [ ] All pages load without errors
- [ ] API calls work (check Network tab)

---

**Backend:** https://mf-backend-bd96.vercel.app
**Frontend:** Will be assigned after deployment
