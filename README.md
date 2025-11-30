# DynamixLMS

Modern learning management system with a **React + TypeScript** frontend and a **Node.js + Express + MongoDB** backend.

## Tech Stack

- **Frontend**: React, TypeScript, Vite, React Router, Tailwind CSS (CDN), Lucide icons, Recharts
- **Backend**: Node.js, Express, MongoDB, Mongoose

## Project Structure

```text
Assignment_1/
  backend/
    server.js
    models/
    package.json
  frontend/
    index.html
    index.tsx
    App.tsx
    components/
      Layout.tsx
    context/
      Store.tsx
    pages/
      Login.tsx
      StudentDashboard.tsx
      TeacherDashboard.tsx
      Catalog.tsx
      CourseView.tsx
      Profile.tsx
    package.json
    vite.config.ts
  README.md
```

## Prerequisites

- Node.js (v18+ recommended)
- npm
- MongoDB running locally on `mongodb://localhost:27017` (or your own URI)

## Backend Setup (API server)

1. Open a terminal in the `backend` folder:

   ```bash
   cd backend
   npm install
   ```

2. (Optional) Create a `.env` file in `backend` if you want to override defaults:

   ```env
   MONGO_URI=mongodb://localhost:27017/dynamixlms
   PORT=5000
   ```

   If you skip this, the app uses the values above by default.

3. Start the backend server (with auto-reload during development):

   ```bash
   npm run dev
   ```

   Or in production mode:

   ```bash
   npm start
   ```

4. On first run, the backend seeds demo data into MongoDB:

   - **Student**: `student@demo.com` / `password`
   - **Teacher**: `teacher@demo.com` / `password`

   The API is exposed at `http://localhost:5000/api` by default.

## Frontend Setup (React app)

1. Open another terminal in the `frontend` folder:

   ```bash
   cd frontend
   npm install
   ```

2. Start the Vite dev server:

   ```bash
   npm run dev
   ```

3. Open the URL printed in the terminal (typically `http://localhost:5173/`).

## Frontend–Backend Connection

The frontend talks to the backend through REST endpoints.

- Base URL is defined in `frontend/context/Store.tsx`:

  ```ts
  const API_URL = 'http://localhost:5000/api';
  ```

- Example calls:
  - `POST  /api/auth/login` – login
  - `POST  /api/auth/register` – register
  - `GET   /api/courses` – list courses
  - `POST  /api/courses` – create course (teacher)
  - `PUT   /api/courses/:id` – update course
  - `DELETE /api/courses/:id` – delete course
  - `GET   /api/enrollments?userId=...` – user enrollments
  - `POST  /api/enrollments` – enroll in a course
  - `PUT   /api/enrollments/progress` – update module completion

Make sure **both** servers are running:

- Backend: `http://localhost:5000`
- Frontend: `http://localhost:5173`

If you change the backend port or host, update `API_URL` in `Store.tsx` accordingly.

## Using the App

### Login

Use the seeded demo accounts or register a new one:

- **Student**: `student@demo.com` / `password`
- **Teacher**: `teacher@demo.com` / `password`

### Student Experience

- **Dashboard**: shows enrolled courses and progress.
- **Browse Courses**: discover and enroll in available courses.
- **Course View**: read module content and complete quizzes.
- **Profile**: view and edit basic user information.

### Instructor (Teacher) Experience

- After logging in as a teacher, you land on the **Instructor Dashboard**.
- The sidebar **Dashboard** item leads to the instructor dashboard (course management view).
- You can:
  - Create courses and modules (with quiz questions).
  - Edit or delete existing courses.
  - See basic enrollment analytics (via charts).

### Session Persistence

- Basic session state is stored in `localStorage` under the key `dynamix_user`.
- Logout clears this value and resets in-memory state.

## Environment & Configuration

- **CORS** is enabled in the backend (`app.use(cors())`), so the frontend at `localhost:5173` can call `localhost:5000`.
- Update `MONGO_URI` and `PORT` in `.env` if you deploy or use a different MongoDB/port.

## Scripts Summary

### Backend (`/backend/package.json`)

- `npm start` – run server with Node.
- `npm run dev` – run server with Nodemon (auto-restart on changes).

### Frontend (`/frontend/package.json`)

- `npm run dev` – start Vite dev server.
- `npm run build` – production build.
- `npm run preview` – preview production build locally.

## Troubleshooting

- If the frontend shows loading/errors for data:
  - Ensure MongoDB is running.
  - Ensure backend is running on the same URL as `API_URL`.
- If `npm run dev` fails in `frontend`, reinstall dependencies:

  ```bash
  cd frontend
  npm install
  ```

- If login fails with demo users, clear browser storage and restart backend to re-run seeding.
