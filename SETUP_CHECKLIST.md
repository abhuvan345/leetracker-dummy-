# MongoDB Atlas Quick Setup Checklist

## ✅ Step-by-Step Checklist

### MongoDB Atlas Setup

- [ ] Create MongoDB Atlas account at https://www.mongodb.com/cloud/atlas/register
- [ ] Create a FREE M0 cluster
- [ ] Wait for cluster to be created (3-5 minutes)
- [ ] Create database user (Security → Database Access)
  - Username: ********\_********
  - Password: ********\_******** (save this!)
- [ ] Add IP address (Security → Network Access)
  - For dev: Allow access from anywhere (0.0.0.0/0)
- [ ] Get connection string (Database → Connect → Connect your application)
  - Copy the string
  - Replace <username> and <password>
  - Add database name: `/leetracker`

### Backend Setup

- [ ] Navigate to backend folder: `cd backend`
- [ ] Install dependencies: `npm install`
- [ ] Create `.env` file from `.env.example`
- [ ] Update `MONGODB_URI` in `.env` with your connection string
- [ ] Start server: `npm run dev`
- [ ] Verify: See "✅ Connected to MongoDB" message
- [ ] Test: Open http://localhost:5000/api/health in browser

### Frontend Setup

- [ ] Navigate to frontend folder: `cd leetracker`
- [ ] Create `.env` file from `.env.example`
- [ ] Add `VITE_API_URL=http://localhost:5000/api`
- [ ] Start frontend: `npm run dev`
- [ ] Open app in browser

### Test Upload

- [ ] Go to Admin page
- [ ] Enter company name (e.g., "Google")
- [ ] Upload a CSV file with questions
- [ ] Check MongoDB Atlas → Browse Collections → questions

### Verify Everything Works

- [ ] Questions appear in Dashboard
- [ ] Can mark questions as complete
- [ ] Stats are calculated correctly
- [ ] Streak calendar updates

---

## 🔗 Your MongoDB Connection Details

**Cluster Name**: **************\_**************

**Connection String**:

```
mongodb+srv://________________:________________@cluster0.xxxxx.mongodb.net/leetracker
```

**Database Name**: leetracker

**Collections**:

- questions
- progresses

---

## 🆘 Need Help?

See detailed instructions in MONGODB_SETUP.md
