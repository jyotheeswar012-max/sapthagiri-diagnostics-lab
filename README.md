# sapthagiri-diagnostics-lab
[README.md](https://github.com/user-attachments/files/26144942/README.md)
# 🏥 Sapthagiri Lab — Full-Stack Portal

**Address:** Munneshwara Block, Kattigenahalli, Sathanur, Bengaluru, Karnataka 560064  
**Contact:** +91 95350 12136

---

## 📁 Project Structure

```
sapthagiri-lab/
├── backend/
│   ├── server.js           ← Main Express server
│   ├── seed.js             ← Database seed script (run once)
│   ├── package.json
│   ├── .env.example        ← Copy this to .env
│   ├── middleware/auth.js  ← JWT authentication
│   ├── models/             ← MongoDB schemas
│   │   ├── User.js
│   │   ├── Patient.js
│   │   ├── Appointment.js
│   │   ├── Report.js
│   │   └── Staff.js
│   └── routes/             ← API endpoints
│       ├── auth.js
│       ├── patients.js
│       ├── appointments.js
│       ├── reports.js
│       ├── staff.js
│       └── analytics.js
└── frontend/
    └── index.html          ← Complete single-file frontend
```

---

## ⚡ Quick Setup (Local)

### Prerequisites
- Node.js v18+
- MongoDB (local or MongoDB Atlas free tier)

### Step 1 — Install backend
```bash
cd backend
npm install
```

### Step 2 — Configure environment
```bash
cp .env.example .env
# Edit .env and set your MONGODB_URI and JWT_SECRET
```

### Step 3 — Seed the database
```bash
npm run seed
```

### Step 4 — Start the server
```bash
npm run dev       # development (auto-restart)
npm start         # production
```

### Step 5 — Open the frontend
Open `frontend/index.html` in your browser, OR serve it:
```bash
cd frontend
npx serve .
```

---

## 🔐 Demo Login Credentials

| Role     | Email                        | Password |
|----------|------------------------------|----------|
| Owner    | owner@sapthagirilab.com      | 1234     |
| Doctor 1 | doctor@gmail.com             | 1234     |
| Doctor 2 | doctor2@gmail.com            | 1234     |
| Patient  | patient@gmail.com            | 1234     |

---

## 🌐 API Endpoints

| Method | Route                           | Access         |
|--------|---------------------------------|----------------|
| POST   | /api/auth/login                 | Public         |
| POST   | /api/auth/register              | Public         |
| GET    | /api/auth/me                    | All            |
| PUT    | /api/auth/profile               | All            |
| GET    | /api/patients                   | Owner/Doctor   |
| POST   | /api/patients                   | Owner          |
| PUT    | /api/patients/:id               | Owner/Doctor   |
| DELETE | /api/patients/:id               | Owner          |
| GET    | /api/appointments               | All            |
| POST   | /api/appointments               | All            |
| PUT    | /api/appointments/:id           | Owner/Doctor/Patient |
| PATCH  | /api/appointments/:id/pay       | Owner          |
| DELETE | /api/appointments/:id           | Owner/Patient  |
| GET    | /api/reports                    | All            |
| POST   | /api/reports                    | Owner/Doctor   |
| PUT    | /api/reports/:id                | Owner/Doctor   |
| POST   | /api/reports/:id/upload         | Owner/Doctor   |
| GET    | /api/reports/:id/download       | All            |
| PATCH  | /api/reports/:id/ready          | Owner/Doctor   |
| GET    | /api/staff                      | Owner          |
| POST   | /api/staff                      | Owner          |
| PUT    | /api/staff/:id                  | Owner          |
| GET    | /api/staff/doctors              | Owner          |
| POST   | /api/staff/doctors              | Owner          |
| PUT    | /api/staff/doctors/:id          | Owner          |
| GET    | /api/analytics                  | Owner          |

---

## 🚀 Production Deployment

### Option A — Render.com (Free)
1. Push code to GitHub
2. Go to https://render.com → New Web Service
3. Set:
   - Build Command: `cd backend && npm install`
   - Start Command: `cd backend && npm start`
4. Add environment variables from `.env`
5. For frontend: New Static Site → point to `/frontend`

### Option B — Railway.app (Easy)
1. Push to GitHub
2. Create project on railway.app
3. Add MongoDB plugin (free tier)
4. Set env vars — Railway auto-detects `PORT`

### Option C — VPS (DigitalOcean / AWS)
```bash

```

### MongoDB Atlas (Free Cloud DB)
1. Go to https://cloud.mongodb.com
2. Create free M0 cluster
3. Get connection string
4. Set `MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/sapthagiri_lab`

---

##  Features

### Owner
- Full dashboard with analytics
- Add / edit / remove patients
- Add / edit / remove doctors and staff
- Manage all appointments (reschedule, cancel, mark complete)
- Mark payments as received (UPI / Card / Cash)
- Add / edit / update reports + upload PDFs
- Revenue analytics with charts

### Doctor
- See only their assigned patients
- View and manage their appointments
- Add and edit reports for their patients
- Upload PDF reports

### Patient
- Book tests online (select tests, date, time, home/walkin)
- View appointment history
- Download ready reports as PDF
- Payment history

