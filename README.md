# Shop Feedback Hub

### A store rating platform that actually makes sense

So you need a way to manage store ratings? We've got you covered. This is a full-stack app that makes collecting and managing store feedback actually enjoyable (yes, really!).

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)
[![Node.js](https://img.shields.io/badge/Node.js-v14+-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![React](https://img.shields.io/badge/React-18.2-61DAFB?logo=react&logoColor=white)](https://reactjs.org/)

---

## What's This All About?

**Shop Feedback Hub** is basically like having a super-organized assistant who keeps track of all your store ratings, manages users, and makes everyone's life easier. Whether you're running the whole show as an admin, owning a store, or just browsing to rate your favorite shops - we've got something for you.

### Why Should You Care?

Look, I could bore you with technical jargon, but here's what really matters:

- **It looks good** - No ugly 90s-style forms here. We've made it clean and modern
- **It's secure** - Your passwords are hashed, your data is protected. We take this seriously
- **Everyone gets their own space** - Admins do admin things, store owners see their metrics, users rate stores. No confusion
- **It actually works on your phone** - Because who even uses just desktop anymore?
- **It's fast** - Nobody has time to wait around for pages to load

---

## What Can You Do With It?

### If You're an Admin

You're basically the puppet master here:

- Create and manage user accounts (both regular users and store owners)
- Add new stores to the platform
- See everything happening in real-time with the dashboard
- Search and filter through users and stores like a pro
- Keep track of how many ratings are rolling in

### If You're a Regular User

Here's your playground:

- Sign up and create your own account (we'll guide you through it)
- Browse through all the stores in the system
- Give ratings from 1 to 5 stars - be honest!
- Change your mind? Update your ratings anytime
- See which stores you've already rated
- Keep your password secure with easy updates

### If You Own a Store

Your personal analytics dashboard:

- See your average rating at a glance
- Check out how many 1-star vs 5-star ratings you're getting
- View everyone who's rated your store
- Sort through customer feedback however you want
- Track your performance over time

---

## What We Built This With

We didn't reinvent the wheel, just used the good stuff:

**Backend:**
- Express.js and Node.js (for the server)
- MySQL (storing all the data)
- JWT (keeping things secure)
- bcrypt (so passwords stay safe)

**Frontend:**
- React 18 (because it's 2024)
- React Router (for navigation)
- Plain CSS3 (keeping it simple)

---

## Getting Started

Alright, let's get you up and running. Don't worry, it's easier than it looks.

### What You'll Need First

Make sure you've got these installed:

- Node.js (version 14 or newer)
- MySQL (version 8.0 or newer)
- npm (comes with Node.js)
- Git

### Setting It Up

**Step 1: Get the code**

```bash
git clone https://github.com/akshatsoni123/Shop-Feedback-Hub.git
cd Shop-Feedback-Hub
```

**Step 2: Install everything**

For the backend:
```bash
npm install
```

For the frontend:
```bash
cd frontend
npm install
cd ..
```

**Step 3: Set up your database**

If you're comfortable with MySQL command line:
```bash
mysql -u root -p
```
Then run:
```sql
source database/schema.sql
exit
```

Or if you prefer phpMyAdmin (like with XAMPP):
1. Open phpMyAdmin in your browser
2. Click the Import tab
3. Choose the `database/schema.sql` file
4. Hit Go and you're done

**Step 4: Configure your environment**

Create a `.env` file in the root folder:

```bash
cp .env.example .env
```

Then edit it with your details:

```env
PORT=5000
NODE_ENV=development

DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password
DB_NAME=store_rating_db

JWT_SECRET=make_this_something_random_and_long
JWT_EXPIRE=24h

CLIENT_URL=http://localhost:3000
```

**Step 5: Fire it up**

Open two terminal windows.

In the first one (backend):
```bash
npm run dev
```

In the second one (frontend):
```bash
cd frontend
npm start
```

Your browser should automatically open to `http://localhost:3000`. If it doesn't, just go there manually.

---

## Your First Login

Here are the default admin credentials:

```
Email: admin@system.com
Password: Admin@123
```

**Important:** Seriously, change these right after you log in for the first time. We're trusting you here.

---

## The Rules (Validation)

We've got some requirements to keep things clean:

- **Names:** Between 20 and 60 characters (yeah, we need full names)
- **Emails:** Has to be a real email format
- **Passwords:** 8-16 characters, at least one uppercase letter and one special character
- **Addresses:** Up to 400 characters

---

## How to Use It

### For Admins

1. Log in with your admin account
2. Head to the Dashboard to see what's happening
3. Click "Add User" to create new accounts
4. Click "Add Store" to register new stores
5. Use the user and store management pages to keep things organized

### For Regular Users

1. Register for an account (it takes like 30 seconds)
2. Log in with your new credentials
3. Browse the stores from your dashboard
4. Click "Rate Store" to give your feedback
5. Want to change your rating? Just click "Update Rating"

### For Store Owners

1. Log in with the credentials the admin gave you
2. Check out your dashboard - all your stats are right there
3. See how customers are rating you
4. View who's giving you those ratings
5. Keep an eye on your performance

---

## API Reference

If you're integrating with our API or just curious, here's what you need to know.

**Base URL:** `http://localhost:5000/api`

### Authentication Stuff

**Register a new user:**
```http
POST /auth/register
```
Send this in the body:
```json
{
  "name": "John Doe Smith Anderson",
  "email": "john@example.com",
  "password": "Password@123",
  "address": "123 Main Street, City"
}
```

**Login:**
```http
POST /auth/login
```
```json
{
  "email": "john@example.com",
  "password": "Password@123"
}
```

You'll get back a token - keep that safe, you'll need it for authenticated requests.

**Get your profile:**
```http
GET /auth/profile
Authorization: Bearer your_token_here
```

**Change your password:**
```http
PUT /auth/update-password
Authorization: Bearer your_token_here
```
```json
{
  "currentPassword": "OldPassword@123",
  "newPassword": "NewPassword@123"
}
```

### Admin Endpoints

All of these need an admin token in the Authorization header.

**Dashboard stats:**
```http
GET /admin/dashboard/stats
```

**Create a user:**
```http
POST /admin/users
```

**Get all users (with optional filters):**
```http
GET /admin/users?name=john&role=user&sortBy=name&sortOrder=ASC
```

**Add a store:**
```http
POST /admin/stores
```

### User Endpoints

Need a user token for these.

**See all stores:**
```http
GET /user/stores?name=electronics&sortBy=average_rating&sortOrder=DESC
```

**Rate a store:**
```http
POST /user/ratings
```
```json
{
  "store_id": 1,
  "rating": 5
}
```

**Update your rating:**
```http
PUT /user/ratings
```
```json
{
  "store_id": 1,
  "rating": 4
}
```

### Store Owner Endpoints

Need a store owner token.

**Your dashboard stats:**
```http
GET /store-owner/dashboard/stats
```

**See who rated you:**
```http
GET /store-owner/ratings/users?sortBy=rating&sortOrder=DESC
```

---

## How the Database Works

We've got three main tables:

**Users** - Stores everyone (admins, regular users, and store owners)
**Stores** - All the stores in the system
**Ratings** - Links users to stores with their ratings

The relationships are pretty straightforward:
- One store owner can have multiple stores
- Users can rate multiple stores
- Each user can only rate each store once (no spam!)

---

## Security

We take security seriously, but we're not paranoid. Here's what we do:

- Passwords are hashed with bcrypt (so we literally can't see your password)
- JWT tokens for authentication (industry standard)
- All database queries use parameterization (no SQL injection here)
- Input validation on both frontend and backend
- Role-based access control (you only see what you're supposed to)

**A few tips:**
- Change that default admin password immediately
- Use a strong, random JWT_SECRET in production
- Enable HTTPS when you go live
- Keep your dependencies updated
- Back up your database regularly

---

## Project Structure

Here's where everything lives:

```
Shop-Feedback-Hub/
├── backend/              (All server-side code)
│   ├── config/          (Database setup)
│   ├── controllers/     (Business logic)
│   ├── middleware/      (Auth and validation)
│   ├── routes/          (API endpoints)
│   └── server.js        (Main server file)
├── database/            (SQL files)
├── frontend/            (React app)
│   └── src/
│       ├── components/  (All React components)
│       ├── context/     (State management)
│       └── services/    (API calls)
├── .env.example         (Environment template)
└── README.md           (You are here)
```