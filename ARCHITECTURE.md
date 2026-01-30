# LeetTracker Architecture

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER BROWSER                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │              React Frontend (Vite)                       │  │
│  │              Port: 5173                                  │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │                                                          │  │
│  │  📊 Dashboard    📝 Questions    ⚙️ Admin               │  │
│  │                                                          │  │
│  │  • View companies                                        │  │
│  │  • Track progress                                        │  │
│  │  • Mark complete                                         │  │
│  │  • Upload CSV                                            │  │
│  │                                                          │  │
│  └────────────────┬─────────────────────────────────────────┘  │
│                   │                                             │
│                   │ HTTP API Calls                              │
│                   │ (fetch)                                     │
└───────────────────┼─────────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                    Express Backend Server                        │
│                    Port: 5000                                    │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  API Routes:                                                     │
│  ┌────────────────────────────────────────────────────────┐    │
│  │ POST   /api/questions/upload                           │    │
│  │ GET    /api/questions                                  │    │
│  │ GET    /api/questions/company/:name                    │    │
│  │ GET    /api/questions/companies/all                    │    │
│  │ DELETE /api/questions/company/:name                    │    │
│  │                                                        │    │
│  │ POST   /api/progress/toggle/:questionId                │    │
│  │ GET    /api/progress/daily                             │    │
│  │ GET    /api/progress/stats                             │    │
│  └────────────────────────────────────────────────────────┘    │
│                                                                  │
│  Models (Mongoose):                                              │
│  • Question.js                                                   │
│  • Progress.js                                                   │
│                                                                  │
└────────────────────────┬────────────────────────────────────────┘
                         │
                         │ Mongoose ODM
                         │ (MongoDB Driver)
                         ▼
┌─────────────────────────────────────────────────────────────────┐
│                    MongoDB Atlas (Cloud)                         │
│                    mongodb+srv://...                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Database: leetracker                                            │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ Collection: questions                                    │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │ {                                                        │  │
│  │   _id: ObjectId,                                         │  │
│  │   title: "Two Sum",                                      │  │
│  │   difficulty: "Easy",                                    │  │
│  │   frequency: 95.5,                                       │  │
│  │   acceptanceRate: 49.2,                                  │  │
│  │   link: "https://...",                                   │  │
│  │   topics: ["Array", "Hash Table"],                       │  │
│  │   company: "Google",                                     │  │
│  │   createdAt: Date,                                       │  │
│  │   updatedAt: Date                                        │  │
│  │ }                                                        │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌──────────────────────────────────────────────────────────┐  │
│  │ Collection: progresses                                   │  │
│  ├──────────────────────────────────────────────────────────┤  │
│  │ {                                                        │  │
│  │   _id: ObjectId,                                         │  │
│  │   questionId: ObjectId (ref to questions),               │  │
│  │   userId: "default-user",                                │  │
│  │   completed: true,                                       │  │
│  │   completedAt: Date,                                     │  │
│  │   createdAt: Date,                                       │  │
│  │   updatedAt: Date                                        │  │
│  │ }                                                        │  │
│  └──────────────────────────────────────────────────────────┘  │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

## Data Flow

### 1. Upload Questions (CSV)

```
Admin Page (React)
    │
    ▼
Upload CSV File + Company Name
    │
    ▼
POST /api/questions/upload
    │
    ▼
Backend parses CSV
    │
    ▼
Save to MongoDB (questions collection)
    │
    ▼
Return success message
    │
    ▼
Display in Dashboard
```

### 2. View Questions

```
Dashboard (React)
    │
    ▼
GET /api/questions/companies/all
    │
    ▼
Backend fetches from MongoDB
    │
    ▼
Aggregate stats per company
    │
    ▼
Return company cards with stats
    │
    ▼
Display in UI
```

### 3. Mark Question Complete

```
Question Table (React)
    │
    ▼
Click checkbox
    │
    ▼
POST /api/progress/toggle/:questionId
    │
    ▼
Backend updates/creates progress record
    │
    ▼
Save to MongoDB (progresses collection)
    │
    ▼
Return new status
    │
    ▼
Update UI
```

## Technology Stack

### Frontend

- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite
- **Styling**: Tailwind CSS + shadcn/ui
- **State Management**: React hooks
- **HTTP Client**: Fetch API
- **Routing**: React Router

### Backend

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database ODM**: Mongoose
- **File Upload**: Multer
- **CORS**: cors middleware
- **Environment**: dotenv

### Database

- **Type**: NoSQL Document Database
- **Service**: MongoDB Atlas (Cloud)
- **Collections**: questions, progresses
- **Indexes**:
  - questions: { title: 1, company: 1 } (unique)
  - progresses: { questionId: 1, userId: 1 } (unique)

## File Structure

```
Leetracer/
├── backend/                    # Node.js Backend
│   ├── models/
│   │   ├── Question.js        # Question schema
│   │   └── Progress.js        # Progress schema
│   ├── routes/
│   │   ├── questions.js       # Question endpoints
│   │   └── progress.js        # Progress endpoints
│   ├── .env                   # Environment config
│   ├── .env.example
│   ├── package.json
│   └── server.js              # Express app
│
└── leetracker/                # React Frontend
    ├── src/
    │   ├── components/
    │   │   └── admin/
    │   │       └── CSVUploader.tsx
    │   ├── lib/
    │   │   ├── api.ts         # API client
    │   │   └── storage.ts     # (legacy localStorage)
    │   ├── pages/
    │   │   ├── Dashboard.tsx
    │   │   ├── Admin.tsx
    │   │   └── CompanyQuestions.tsx
    │   └── types/
    │       └── question.ts
    ├── .env
    ├── .env.example
    └── package.json
```

## Environment Variables

### Backend (.env)

```
MONGODB_URI=mongodb+srv://username:password@cluster0.xxxxx.mongodb.net/leetracker
PORT=5000
NODE_ENV=development
```

### Frontend (.env)

```
VITE_API_URL=http://localhost:5000/api
```

## Security Considerations

### Current (Development)

- ✅ CORS enabled for all origins
- ✅ MongoDB allows all IPs (0.0.0.0/0)
- ✅ Single user (no authentication)

### Production Recommendations

- 🔒 Restrict CORS to specific domains
- 🔒 Whitelist specific IP addresses in MongoDB
- 🔒 Add user authentication (JWT)
- 🔒 Rate limiting on API endpoints
- 🔒 Input validation and sanitization
- 🔒 HTTPS/SSL certificates
- 🔒 Environment variable management
