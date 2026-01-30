# 🔧 Troubleshooting Guide - Data Not Showing

## Issue Fixed! ✅

Your frontend was still using localStorage instead of the MongoDB API. I've updated:

- ✅ Dashboard.tsx - Now fetches from API
- ✅ CompanyQuestions.tsx - Now fetches from API
- ✅ AllQuestions.tsx - Now fetches from API
- ✅ QuestionTable.tsx - Now toggles via API
- ✅ CompanyManager.tsx - Now manages via API
- ✅ Backend .env - Added database name `/leetracker`

---

## 🚀 Next Steps to See Your Data

### 1. Restart Backend Server

Open terminal in backend folder:

```powershell
cd C:\Users\bhuvan\Desktop\Leetracer\backend

# Stop current server (Ctrl+C if running)
# Then start it again:
npm run dev
```

**You should see:**

```
✅ Connected to MongoDB
🚀 Server running on http://localhost:5000
```

### 2. Restart Frontend Server

Open NEW terminal in leetracker folder:

```powershell
cd C:\Users\bhuvan\Desktop\Leetracer\leetracker

# Stop current server (Ctrl+C if running)
# Then start it again:
npm run dev
```

### 3. Test Backend API

In backend folder, run:

```powershell
.\test-api.ps1
```

This will show you:

- ✅ If backend is running
- ✅ How many companies in database
- ✅ How many questions in database

### 4. Open Frontend

1. Open browser: http://localhost:5173
2. Press F12 to open DevTools
3. Go to **Console** tab
4. Go to **Dashboard** page
5. Check for any errors

---

## 🔍 Debugging Checklist

### Backend Running?

```powershell
# Test health endpoint
curl http://localhost:5000/api/health
```

**Expected:** `{"status":"ok","message":"Server is running"}`

### MongoDB Connected?

Check backend terminal for:

```
✅ Connected to MongoDB
```

If you see error, check:

- [ ] MONGODB_URI in backend/.env has `/leetracker` in it
- [ ] Username and password are correct
- [ ] Network access allows your IP in MongoDB Atlas

### Frontend Configured?

Check `leetracker/.env` contains:

```
VITE_API_URL=http://localhost:5000/api
```

### Data in MongoDB?

1. Go to MongoDB Atlas dashboard
2. Click **"Browse Collections"**
3. Select `leetracker` database
4. Check `questions` collection has data

### Browser Console Errors?

Press F12 in browser, check Console tab for:

- ❌ CORS errors → Backend not running
- ❌ 404 errors → Check API URL in .env
- ❌ Network errors → Check both servers are running

---

## 🧪 Test the Full Flow

### Step 1: Upload Questions (if not done)

1. Go to http://localhost:5173/admin
2. Enter company name: "TestCompany"
3. Upload a CSV file
4. You should see success message

### Step 2: Check Backend

```powershell
# In backend folder
.\test-api.ps1
```

Should show: `1 company, X questions`

### Step 3: Check Dashboard

1. Go to http://localhost:5173
2. You should see "TestCompany" card
3. Click on it
4. You should see all questions

### Step 4: Test Completion

1. Click checkbox on a question
2. Check MongoDB Atlas → `progresses` collection
3. Should see a new document

---

## 📊 Network Tab Check

1. Open browser DevTools (F12)
2. Go to **Network** tab
3. Refresh Dashboard page
4. You should see these requests:

```
✅ companies/all  → 200 OK → Returns company list
✅ daily          → 200 OK → Returns progress
✅ stats          → 200 OK → Returns statistics
```

Click on each request to see the response data.

---

## 🐛 Common Issues & Solutions

### Issue: "Cannot GET /api/questions"

**Solution:** Backend server not running

```powershell
cd backend
npm run dev
```

### Issue: "CORS policy blocked"

**Solution:**

- Backend must run on port 5000
- Check `cors()` is in server.js (it is)
- Restart backend server

### Issue: "Failed to fetch"

**Solution:**

- Check frontend .env has correct API URL
- Restart frontend: Ctrl+C, then `npm run dev`
- Check browser console for actual error

### Issue: Data shows in MongoDB but not frontend

**Solution:**

- Hard refresh browser: Ctrl+Shift+R
- Clear browser cache
- Check Network tab for failed requests
- Verify API returns data: http://localhost:5000/api/questions

### Issue: Questions upload but count shows 0

**Solution:**

- Check if response shows: `{inserted: 5, skipped: 0}`
- Go to MongoDB Atlas → Browse Collections
- Verify data is actually there
- Refresh frontend page

---

## 🔬 Advanced Debugging

### Check API Response Manually

Open PowerShell and test:

```powershell
# Get all companies
Invoke-RestMethod -Uri "http://localhost:5000/api/questions/companies/all"

# Get all questions
Invoke-RestMethod -Uri "http://localhost:5000/api/questions"

# Get specific company
Invoke-RestMethod -Uri "http://localhost:5000/api/questions/company/Google"
```

### Check MongoDB Data

1. MongoDB Atlas → Database → Browse Collections
2. Database: `leetracker`
3. Collections:
   - `questions` - Should have your questions
   - `progresses` - Will have completion records

### Enable Verbose Logging

Add console.log to your API calls:

Edit `leetracker/src/lib/api.ts`, add before return:

```typescript
console.log("API Response:", response);
```

---

## ✅ Success Indicators

You'll know it's working when:

1. **Backend terminal shows:**

   ```
   ✅ Connected to MongoDB
   🚀 Server running on http://localhost:5000
   ```

2. **Frontend loads without errors**
   - No red errors in Console (F12)
   - Companies appear on Dashboard
   - Questions appear when clicking company

3. **Network tab shows successful requests**
   - All API calls return 200 status
   - Responses contain data

4. **MongoDB Atlas shows data**
   - `questions` collection has documents
   - Documents match what you uploaded

---

## 📞 Still Not Working?

Run this diagnostic:

```powershell
# In backend folder
Write-Host "Backend Status:" -ForegroundColor Cyan
Get-Process -Name node -ErrorAction SilentlyContinue | Select-Object Id, ProcessName

Write-Host "`nTesting API:" -ForegroundColor Cyan
try {
    $response = Invoke-RestMethod -Uri "http://localhost:5000/api/health"
    Write-Host "✅ Backend is running" -ForegroundColor Green

    $questions = Invoke-RestMethod -Uri "http://localhost:5000/api/questions"
    Write-Host "✅ Questions API works: $($questions.Count) questions" -ForegroundColor Green
} catch {
    Write-Host "❌ API Error: $_" -ForegroundColor Red
}
```

Share the output if you need more help!

---

## 🎯 Quick Fix Commands

```powershell
# Restart everything
cd C:\Users\bhuvan\Desktop\Leetracer

# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd leetracker
npm run dev

# Terminal 3 - Test
cd backend
.\test-api.ps1
```

Then open: http://localhost:5173
