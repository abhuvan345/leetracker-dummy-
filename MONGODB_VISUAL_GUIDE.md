# MongoDB Atlas Setup - Visual Guide

## Step 1: Create Account

1. Go to: https://www.mongodb.com/cloud/atlas/register
2. Sign up options:
   - Google account (recommended - fastest)
   - Email + password
   - GitHub account

```
┌─────────────────────────────────────────┐
│  Welcome to MongoDB Atlas               │
├─────────────────────────────────────────┤
│                                         │
│  [ Sign in with Google ]                │
│                                         │
│  ─────────── OR ───────────             │
│                                         │
│  Email: [________________]              │
│  Password: [____________]               │
│                                         │
│  [  Sign Up  ]                          │
└─────────────────────────────────────────┘
```

---

## Step 2: Create Cluster

After login, you'll see "Create a deployment"

### Choose Cluster Tier:

```
┌───────────────────────────────────────────────────┐
│  Deploy a cloud database                          │
├───────────────────────────────────────────────────┤
│                                                   │
│  ┌─────────────────────────────────────────┐     │
│  │  M0                          FREE       │ ✓   │
│  │  Shared RAM                             │     │
│  │  512 MB Storage                         │     │
│  │  Shared vCPU                            │     │
│  │                                         │     │
│  │  Perfect for learning and exploring     │     │
│  └─────────────────────────────────────────┘     │
│                                                   │
│  ┌─────────────────────────────────────────┐     │
│  │  M10                    $57/month       │     │
│  │  2 GB RAM                               │     │
│  │  10 GB Storage                          │     │
│  └─────────────────────────────────────────┘     │
│                                                   │
└───────────────────────────────────────────────────┘
```

**✅ Select: M0 (FREE)**

### Choose Provider & Region:

```
┌──────────────────────────────────────────┐
│  Cloud Provider & Region                 │
├──────────────────────────────────────────┤
│                                          │
│  Provider:                               │
│    ⦿ AWS        ○ Google Cloud  ○ Azure │
│                                          │
│  Region:                                 │
│    ▼ us-east-1 (N. Virginia)            │
│       us-west-2 (Oregon)                 │
│       eu-west-1 (Ireland)                │
│       ap-south-1 (Mumbai)                │
│                                          │
│  💡 Choose region closest to you         │
└──────────────────────────────────────────┘
```

**✅ Choose region closest to your location**

### Cluster Name:

```
┌──────────────────────────────────────────┐
│  Cluster Name                            │
├──────────────────────────────────────────┤
│                                          │
│  [leetracker-cluster___________]         │
│                                          │
│  (or any name you like)                  │
└──────────────────────────────────────────┘
```

**✅ Click "Create Deployment"**

⏱️ **Wait 3-5 minutes for cluster creation**

---

## Step 3: Create Database User

You'll see a popup: "Security Quickstart"

### Create Database User:

```
┌──────────────────────────────────────────────┐
│  Security Quickstart                         │
├──────────────────────────────────────────────┤
│                                              │
│  How would you like to authenticate?        │
│                                              │
│  ⦿ Username and Password                    │
│  ○ Certificate                               │
│                                              │
│  Username:                                   │
│  [leetracker-admin______________]            │
│                                              │
│  Password:                                   │
│  [**********************]  [Autogenerate]    │
│                                              │
│  💡 IMPORTANT: Save this password!           │
│                                              │
│  [ Create User ]                             │
└──────────────────────────────────────────────┘
```

**Important:**

1. ✅ Choose a strong username (e.g., `leetracker-admin`)
2. ✅ Click "Autogenerate Secure Password" OR create your own
3. ✅ **COPY AND SAVE THE PASSWORD IMMEDIATELY**
4. ✅ Store it in a safe place (password manager recommended)

---

## Step 4: Network Access

Still in the "Security Quickstart" popup:

### Add IP Address:

```
┌──────────────────────────────────────────────┐
│  Where would you like to connect from?       │
├──────────────────────────────────────────────┤
│                                              │
│  ⦿ My Local Environment                     │
│  ○ Cloud Environment                         │
│                                              │
│  IP Access List:                             │
│                                              │
│  Add entries to your IP Access List         │
│                                              │
│  ┌────────────────────────────────────────┐ │
│  │  IP Address: [0.0.0.0/0______________] │ │
│  │  Description: [Allow all IPs_________] │ │
│  │                                        │ │
│  │  ⚠️ For development only!              │ │
│  └────────────────────────────────────────┘ │
│                                              │
│  [ Add Entry ]                               │
│                                              │
│  [ Finish and Close ]                        │
└──────────────────────────────────────────────┘
```

**For Development:**

- IP Address: `0.0.0.0/0` (allows all IPs)
- Description: `Development - Allow all`

**⚠️ Warning:** This is NOT secure for production! Only use while learning.

**For Production:**

- Add specific IP addresses of your servers

---

## Step 5: Get Connection String

After setup completes:

### Navigate to Connect:

```
┌─────────────────────────────────────────────────┐
│  Database Deployments                           │
├─────────────────────────────────────────────────┤
│                                                 │
│  leetracker-cluster                 ⚡ Active   │
│  ┌───────────────────────────────────────────┐ │
│  │  M0 Sandbox • AWS • us-east-1            │ │
│  │  ───────────────────────────────────────  │ │
│  │                                           │ │
│  │  [ Connect ]  [ Browse Collections ]      │ │
│  └───────────────────────────────────────────┘ │
└─────────────────────────────────────────────────┘
```

**✅ Click "Connect" button**

### Choose Connection Method:

```
┌──────────────────────────────────────────────┐
│  Connect to leetracker-cluster               │
├──────────────────────────────────────────────┤
│                                              │
│  [ Drivers ]                                 │ ✓
│    Connect your application                  │
│                                              │
│  [ MongoDB Shell ]                           │
│    Access your data with MongoDB Shell       │
│                                              │
│  [ Compass ]                                 │
│    Use MongoDB Compass GUI                   │
│                                              │
│  [ MongoDB for VS Code ]                     │
│    Access data from VS Code                  │
└──────────────────────────────────────────────┘
```

**✅ Click "Drivers"**

### Get Connection String:

```
┌──────────────────────────────────────────────────┐
│  Connect to your application                     │
├──────────────────────────────────────────────────┤
│                                                  │
│  Driver: Node.js                     ▼           │
│  Version: 5.5 or later               ▼           │
│                                                  │
│  ─────────────────────────────────────────────  │
│                                                  │
│  Connection string:                              │
│                                                  │
│  ┌────────────────────────────────────────────┐ │
│  │ mongodb+srv://leetracker-admin:<password>  │ │
│  │ @cluster0.xxxxx.mongodb.net/                │ │
│  │ ?retryWrites=true&w=majority                │ │
│  │                                    [Copy]   │ │
│  └────────────────────────────────────────────┘ │
│                                                  │
│  Replace <password> with your actual password   │
│                                                  │
└──────────────────────────────────────────────────┘
```

**Steps:**

1. ✅ Copy the connection string
2. ✅ Replace `<password>` with your saved password
3. ✅ Add database name at the end: `/leetracker`

**Final connection string should look like:**

```
mongodb+srv://leetracker-admin:YourPassword123@cluster0.xxxxx.mongodb.net/leetracker?retryWrites=true&w=majority
```

---

## Step 6: Test Connection

### Update Backend .env:

```
MONGODB_URI=mongodb+srv://leetracker-admin:YourPassword123@cluster0.xxxxx.mongodb.net/leetracker?retryWrites=true&w=majority
PORT=5000
NODE_ENV=development
```

### Start Backend:

```powershell
cd backend
npm run dev
```

### Expected Output:

```
> leetracker-backend@1.0.0 dev
> nodemon server.js

[nodemon] 3.0.1
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,json
[nodemon] starting `node server.js`
✅ Connected to MongoDB
🚀 Server running on http://localhost:5000
```

**✅ SUCCESS!** You're connected to MongoDB!

---

## Troubleshooting Visual Guide

### ❌ Authentication Failed

```
Error: MongoServerError: bad auth
Authentication failed
```

**Solution:**

1. Go to Database Access
2. Click "Edit" on your user
3. Click "Edit Password"
4. Generate new password
5. Save password
6. Update .env file
7. Restart server

---

### ❌ Network Error

```
Error: MongoNetworkError: connection refused
Could not connect to any servers
```

**Solution:**

1. Go to Network Access
2. Check if 0.0.0.0/0 is listed
3. If not, click "Add IP Address"
4. Click "Allow Access from Anywhere"
5. Click "Confirm"
6. Wait 2 minutes
7. Restart server

---

### ❌ Database Not Found

```
Error: Database 'leetracker' not found
```

**Solution:**
This is OK! Database will be created automatically when you:

1. Upload your first CSV
2. MongoDB creates collections automatically

---

## Visual Database Structure

After uploading questions, your database will look like:

```
MongoDB Atlas
└── Clusters
    └── leetracker-cluster
        └── Databases
            └── leetracker
                ├── questions
                │   ├── Document 1
                │   │   ├── _id: "65b..."
                │   │   ├── title: "Two Sum"
                │   │   ├── difficulty: "Easy"
                │   │   ├── company: "Google"
                │   │   └── ...
                │   ├── Document 2
                │   └── Document 3...
                │
                └── progresses
                    ├── Document 1
                    │   ├── _id: "65c..."
                    │   ├── questionId: "65b..."
                    │   ├── completed: true
                    │   └── completedAt: "2026-01-30"
                    └── Document 2...
```

---

## Next Steps Checklist

After MongoDB is set up:

- [ ] ✅ Cluster created and running
- [ ] ✅ Database user created
- [ ] ✅ Password saved securely
- [ ] ✅ Network access configured (0.0.0.0/0)
- [ ] ✅ Connection string copied
- [ ] ✅ Connection string in backend/.env
- [ ] ✅ Backend server running
- [ ] ✅ See "Connected to MongoDB" message

**→ Now proceed to:** [README.md](README.md) Step 5 (Frontend setup)

---

## Useful MongoDB Atlas Links

- **Dashboard**: https://cloud.mongodb.com/
- **Browse Collections**: Database → Browse Collections
- **Monitor**: Database → Metrics
- **Database Access**: Security → Database Access
- **Network Access**: Security → Network Access
