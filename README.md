# 🏥 Sapthagiri Lab — Full-Stack Diagnostic Portal

**Lab Name:** Sapthagiri Lab  
**Address:** Munneshwara Block, Kattigenahalli, Sathanur, Bengaluru, Karnataka 560064  
**Phone:** +91 95350 12136  
**Email:** info@sapthagirilab.com  

---

## 📁 Project Structure

```
sapthagiri-lab/
├── backend/
│   ├── server.js              ← Main Express server (port 5000)
│   ├── seed.js                ← Seed database with demo data (run once)
│   ├── package.json
│   ├── .env.example           ← Copy to .env and fill in your keys
│   ├── middleware/
│   │   └── auth.js            ← JWT authentication + query-param token support
│   ├── models/                ← MongoDB/Mongoose schemas
│   │   ├── User.js
│   │   ├── Patient.js
│   │   ├── Appointment.js
│   │   ├── Report.js
│   │   └── Staff.js
│   ├── routes/                ← REST API route handlers
│   │   ├── auth.js
│   │   ├── patients.js
│   │   ├── appointments.js
│   │   ├── reports.js
│   │   ├── staff.js
│   │   ├── payments.js        ← Razorpay payment integration
│   │   └── analytics.js
│   └── services/              ← Shared business-logic services
│       ├── sms.js             ← MSG91 SMS notifications
│       └── pdf.js             ← Auto-generate report / slip / receipt PDFs
└── frontend/
    └── index.html             ← Complete single-file frontend (no build needed)
```

---

## ⚡ Quick Setup (Local)

### Prerequisites
- Node.js v18+
- MongoDB installed locally **or** a free [MongoDB Atlas](https://cloud.mongodb.com) cluster

### Step 1 — Install dependencies
```bash
cd backend
npm install
```

### Step 2 — Configure environment
```bash
cp .env.example .env
# Open .env and fill in MONGODB_URI, JWT_SECRET, and optional keys
```

### Step 3 — Seed the database with demo data
```bash
npm run seed
```

### Step 4 — Start the backend server
```bash
npm run dev      # Development mode (auto-restart on changes)
npm start        # Production mode
```

### Step 5 — Open the frontend
Simply open `frontend/index.html` in your browser.  
Or serve it locally:
```bash
cd frontend
npx serve .
```

> **Important:** Before deploying, change the `BASE` constant near the top of the
> `<script>` section in `frontend/index.html` to your deployed backend URL.
> Example: `const BASE = 'https://your-backend.onrender.com/api';`

---

## 🔐 Demo Login Credentials

All demo accounts use password: **`1234`**

| Role      | Email                         | Password |
|-----------|-------------------------------|----------|
| Owner     | owner@sapthagirilab.com       | 1234     |
| Doctor 1  | doctor@sapthagirilab.com      | 1234     |
| Doctor 2  | doctor2@sapthagirilab.com     | 1234     |
| Patient 1 | patient@sapthagirilab.com     | 1234     |
| Patient 2 | patient2@sapthagirilab.com    | 1234     |

---

## 🌐 API Endpoints

### Auth
| Method | Route                     | Access  | Description                     |
|--------|---------------------------|---------|----------------------------------|
| POST   | /api/auth/login           | Public  | Login and receive JWT token      |
| POST   | /api/auth/register        | Public  | Patient self-registration        |
| GET    | /api/auth/me              | All     | Get current user profile         |
| PUT    | /api/auth/profile         | All     | Update own profile               |
| PUT    | /api/auth/change-password | All     | Change own password              |

### Patients
| Method | Route                        | Access        |
|--------|------------------------------|---------------|
| GET    | /api/patients                | Owner/Doctor  |
| GET    | /api/patients/meta/doctors   | All           |
| GET    | /api/patients/:id            | Owner/Doctor  |
| POST   | /api/patients                | Owner         |
| PUT    | /api/patients/:id            | Owner/Doctor  |
| DELETE | /api/patients/:id            | Owner         |

### Appointments
| Method | Route                                    | Access               |
|--------|------------------------------------------|----------------------|
| GET    | /api/appointments                        | All (role-filtered)  |
| GET    | /api/appointments/schedule/doctor/:id    | Owner/Doctor         |
| GET    | /api/appointments/:id                    | All                  |
| GET    | /api/appointments/:id/slip               | All (PDF download)   |
| POST   | /api/appointments                        | All                  |
| PUT    | /api/appointments/:id                    | Owner/Doctor/Patient |
| PATCH  | /api/appointments/:id/pay               | Owner                |
| DELETE | /api/appointments/:id                    | Owner/Patient        |

### Reports
| Method | Route                        | Access        |
|--------|------------------------------|---------------|
| GET    | /api/reports                 | All (role-filtered) |
| GET    | /api/reports/:id             | All           |
| GET    | /api/reports/:id/pdf         | All (auto-generated PDF) |
| GET    | /api/reports/:id/download    | All (uploaded or auto PDF) |
| POST   | /api/reports                 | Owner/Doctor  |
| PUT    | /api/reports/:id             | Owner/Doctor  |
| POST   | /api/reports/:id/upload      | Owner/Doctor  |
| PATCH  | /api/reports/:id/ready       | Owner/Doctor  |
| DELETE | /api/reports/:id             | Owner         |

### Staff & Doctors
| Method | Route                    | Access |
|--------|--------------------------|--------|
| GET    | /api/staff               | Owner  |
| POST   | /api/staff               | Owner  |
| PUT    | /api/staff/:id           | Owner  |
| DELETE | /api/staff/:id           | Owner  |
| GET    | /api/staff/doctors       | Owner  |
| POST   | /api/staff/doctors       | Owner  |
| PUT    | /api/staff/doctors/:id   | Owner  |
| DELETE | /api/staff/doctors/:id   | Owner  |

### Payments (Razorpay)
| Method | Route                         | Access | Description                      |
|--------|-------------------------------|--------|----------------------------------|
| POST   | /api/payments/create-order    | All    | Create Razorpay payment order    |
| POST   | /api/payments/verify          | All    | Verify signature & mark paid     |
| GET    | /api/payments/receipt/:id     | All    | Download payment receipt PDF     |

### Analytics
| Method | Route           | Access | Description                     |
|--------|-----------------|--------|---------------------------------|
| GET    | /api/analytics  | Owner  | Revenue, counts, charts data    |

---

## 🚀 Production Deployment

### Option A — Render.com (Recommended — Free tier)
1. Push the project to GitHub
2. Go to [render.com](https://render.com) → **New Web Service**
3. Set:
   - **Root Directory:** `backend`
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
4. Add all environment variables from `.env`
5. Create a separate **Static Site** → root directory: `frontend`
6. In `frontend/index.html`, update `const BASE = 'https://your-backend.onrender.com/api';`

### Option B — Railway.app
1. Push to GitHub
2. Create a new project at [railway.app](https://railway.app)
3. Add a **MongoDB** database plugin (free tier available)
4. Set environment variables — Railway auto-detects `PORT`
5. Deploy backend from the `backend/` folder

### Option C — VPS (DigitalOcean / AWS / any Linux server)
```bash
# Install PM2 globally
npm install -g pm2

# Start backend
cd backend
pm2 start server.js --name sapthagiri-lab
pm2 save
pm2 startup   # auto-start on reboot

# Serve frontend with nginx
# Set nginx root to /path/to/sapthagiri-lab/frontend/
```

### MongoDB Atlas (Free Cloud Database)
1. Go to [cloud.mongodb.com](https://cloud.mongodb.com)
2. Create a free **M0** cluster
3. Create a database user and whitelist your IP (or use 0.0.0.0/0 for open access)
4. Copy the connection string and set in `.env`:
   ```
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/sapthagiri_lab
   ```

---

## 🔑 Environment Variables

Copy `.env.example` to `.env` and fill in:

```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/sapthagiri_lab
JWT_SECRET=change_this_to_a_long_random_string_in_production
JWT_EXPIRE=7d
NODE_ENV=development

# MSG91 SMS — get keys from https://msg91.com
MSG91_AUTH_KEY=your_msg91_auth_key
MSG91_SENDER_ID=SPTLAB

# Razorpay Payments — get keys from https://razorpay.com
RAZORPAY_KEY_ID=rzp_test_xxxxxxxxxx
RAZORPAY_KEY_SECRET=your_razorpay_secret

# Lab Info (used in generated PDFs)
LAB_NAME=Sapthagiri Lab
LAB_ADDRESS=Munneshwara Block, Kattigenahalli, Sathanur, Bengaluru 560064
LAB_PHONE=+91 95350 12136
LAB_EMAIL=info@sapthagirilab.com
```

> If MSG91 or Razorpay keys are not set, the app runs in **demo mode** —
> SMS is logged to the console and payments are simulated without real transactions.

---

## ✅ Features

### 👑 Owner Dashboard
- Full analytics: revenue, appointment volume, top tests (charts)
- Add / edit / deactivate patients
- Add / edit / deactivate doctors and lab staff
- View and manage all appointments (reschedule, cancel, mark completed)
- Mark bills as paid (Cash / UPI / Card / Razorpay)
- Create, edit, and upload PDF reports
- Doctor schedule calendar view (all doctors)
- Download appointment slips and payment receipts as PDF
- SMS notifications sent automatically on key events

### 🩺 Doctor Dashboard
- Sees **only their own assigned patients** — cannot see other doctors' patients
- Monthly schedule calendar with appointment dots per day
- Add and edit reports for their own patients
- Upload PDF report files
- Mark reports as ready (triggers SMS to patient)

### 👤 Patient Portal
- Self-registration with email, phone, age, gender, blood group
- Book diagnostic tests (select tests, date, time, walk-in or home collection)
- View all past and upcoming appointments
- Download ready reports as PDF (auto-generated, no upload needed)
- Pay outstanding bills online via Razorpay (UPI / Card / Net Banking)
- Download payment receipts
- Print or download appointment slip

### 🆕 New Features (v2)
- 🌙 Dark mode toggle (persisted across sessions)
- 📱 SMS notifications via MSG91 for booking, reports, payments, cancellations
- 📄 Auto-generated professional PDFs — reports, appointment slips, receipts
- 💳 Razorpay online payment with signature verification
- 📆 Doctor schedule calendar (monthly view, click date for details)
- 🖨 Print appointment slip from any browser
- 👤 Patient self-registration page on landing

---

