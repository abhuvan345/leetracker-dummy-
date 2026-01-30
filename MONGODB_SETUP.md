# MongoDB Integration - Complete Setup Guide

## 📋 Overview

Your LeetCode tracker now has MongoDB integration with a full backend API. Questions are stored in the cloud instead of browser localStorage.

---

## 🗄️ MongoDB Atlas Setup

### Step 1: Create MongoDB Account

1. Go to https://www.mongodb.com/cloud/atlas/register
2. Sign up with email or Google account
3. Select the **FREE** tier

### Step 2: Create a Cluster

1. Click **"Build a Database"**
2. Choose **M0 FREE** tier
3. Select:
   - **Cloud Provider**: AWS (or any)
   - **Region**: Choose closest to you (e.g., US East, Europe West)
4. Cluster Name: `leetracker-cluster` (or any name)
5. Click **"Create"**
6. Wait 3-5 minutes for cluster creation

### Step 3: Create Database User

1. In the **Security** section, click **"Database Access"**
2. Click **"Add New Database User"**
3. Select **"Password"** authentication method
4. Create credentials:
   - **Username**: `leetracker-admin` (example)
   - **Password**: Generate a strong password (SAVE THIS!)
5. Database User Privileges: **"Atlas admin"** or **"Read and write to any database"**
6. Click **"Add User"**

### Step 4: Configure Network Access

1. Go to **"Network Access"** in the left sidebar
2. Click **"Add IP Address"**
3. For development: Click **"Allow Access from Anywhere"**
   - This adds `0.0.0.0/0` (not recommended for production)
4. For production: Add your server's specific IP address
5. Click **"Confirm"**

### Step 5: Get Connection String

1. Go to **"Database"** → Click **"Connect"** on your cluster
2. Choose **"Connect your application"**
3. Select:
   - **Driver**: Node.js
   - **Version**: 5.5 or later
4. Copy the connection string. It looks like:
   ```
   mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/?retryWrites=true&w=majority
   ```
5. **Important**: Replace `<username>` and `<password>` with your actual credentials
6. Add database name at the end:
   ```
   mongodb+srv://leetracker-admin:yourpassword@cluster0.xxxxx.mongodb.net/leetracker?retryWrites=true&w=majority
   ```

---

## 🚀 Backend Setup

### Step 1: Install Dependencies

```powershell
cd C:\Users\bhuvan\Desktop\Leetracer\backend
npm install
```

### Step 2: Configure Environment

```powershell
# Copy the example file
cp .env.example .env

# Edit .env file with your MongoDB connection string
notepad .env
```

In the `.env` file, add:

```
MONGODB_URI=mongodb+srv://leetracker-admin:yourpassword@cluster0.xxxxx.mongodb.net/leetracker?retryWrites=true&w=majority
PORT=5000
NODE_ENV=development
```

### Step 3: Start Backend Server

```powershell
npm run dev
```

You should see:

```
✅ Connected to MongoDB
🚀 Server running on http://localhost:5000
```

---

## 💻 Frontend Setup

### Step 1: Configure Environment

```powershell
cd C:\Users\bhuvan\Desktop\Leetracer\leetracker

# Create .env file
cp .env.example .env

# Edit .env
notepad .env
```

Add this to `.env`:

```
VITE_API_URL=http://localhost:5000/api
```

### Step 2: Start Frontend

```powershell
npm run dev
```

---

## 📊 Database Collections

Your MongoDB database will have these collections:

### 1. `questions` Collection

```javascript
{
  _id: ObjectId("..."),
  title: "Two Sum",
  difficulty: "Easy",
  frequency: 95.5,
  acceptanceRate: 49.2,
  link: "https://leetcode.com/problems/two-sum/",
  topics: ["Array", "Hash Table"],
  company: "Google",
  createdAt: ISODate("2026-01-30T..."),
  updatedAt: ISODate("2026-01-30T...")
}
```

### 2. `progresses` Collection

```javascript
{
  _id: ObjectId("..."),
  questionId: ObjectId("..."), // Reference to questions
  userId: "default-user",
  completed: true,
  completedAt: ISODate("2026-01-30T..."),
  createdAt: ISODate("2026-01-30T..."),
  updatedAt: ISODate("2026-01-30T...")
}
```

---

## 🔌 API Endpoints

### Questions

- `POST /api/questions/upload` - Upload CSV with questions
- `GET /api/questions` - Get all questions
- `GET /api/questions/company/:companyName` - Get company questions
- `GET /api/questions/companies/all` - Get all companies with stats
- `DELETE /api/questions/company/:companyName` - Delete company questions

### Progress

- `POST /api/progress/toggle/:questionId` - Toggle completion
- `GET /api/progress/daily` - Get daily progress
- `GET /api/progress/stats` - Get statistics

---

## 📁 CSV Upload Format

Your CSV should have these headers:

```csv
Title,Difficulty,Frequency,Acceptance Rate,Link,Topics
Two Sum,Easy,95.5,49.2,https://leetcode.com/problems/two-sum/,"Array,Hash Table"
Add Two Numbers,Medium,82.3,41.8,https://leetcode.com/problems/add-two-numbers/,"Linked List,Math"
```

**Headers** (case-insensitive):

- `Title` - Question name
- `Difficulty` - Easy/Medium/Hard
- `Frequency` - Number (how often asked)
- `Acceptance Rate` - Percentage
- `Link` - LeetCode URL
- `Topics` - Comma-separated tags

---

## ✅ Testing the Setup

### 1. Test Backend Health

Open browser: http://localhost:5000/api/health

Should see:

```json
{ "status": "ok", "message": "Server is running" }
```

### 2. Upload Questions

1. Go to Admin page in your app
2. Enter company name (e.g., "Google")
3. Upload a CSV file
4. Check MongoDB Atlas:
   - Go to **"Browse Collections"**
   - You should see `questions` collection with data

### 3. View Questions

1. Go to Dashboard
2. You should see the company card
3. Click on it to view questions

---

## 🐛 Troubleshooting

### "MongooseError: no connection string provided"

- Make sure `.env` file exists in backend folder
- Check `MONGODB_URI` is set correctly
- Restart the server after changing `.env`

### "MongoNetworkError: failed to connect"

- Check your Network Access in MongoDB Atlas
- Ensure IP address `0.0.0.0/0` is allowed
- Verify connection string is correct

### "Authentication failed"

- Double-check username and password in connection string
- Make sure password doesn't contain special characters (or URL-encode them)
- Verify user has proper permissions in MongoDB Atlas

### CORS errors in frontend

- Make sure backend server is running on port 5000
- Check VITE_API_URL in frontend `.env`
- Verify `cors()` is enabled in backend

---

## 🔒 Security Notes

### For Development:

✅ Allow access from anywhere (0.0.0.0/0)
✅ Use `.env` files (never commit to Git)

### For Production:

❌ Don't allow access from anywhere
✅ Whitelist specific IP addresses
✅ Use strong passwords
✅ Enable MongoDB encryption
✅ Add user authentication to your app
✅ Use environment variables in hosting platform

---

## 🎯 Next Steps

1. ✅ Set up MongoDB Atlas
2. ✅ Configure backend with connection string
3. ✅ Start backend server
4. ✅ Configure frontend API URL
5. ✅ Test CSV upload
6. 📝 Add user authentication (optional)
7. 🚀 Deploy to production

---

## 📚 Resources

- [MongoDB Atlas Docs](https://www.mongodb.com/docs/atlas/)
- [Mongoose Docs](https://mongoosejs.com/docs/guide.html)
- [Express.js Guide](https://expressjs.com/en/guide/routing.html)
