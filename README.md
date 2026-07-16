<div align="center">

# 🚌 RedBus Clone

### Online Bus Ticket Booking Platform

A full-stack bus booking application inspired by RedBus — search routes, pick seats, pay with Razorpay, and manage your bookings.

<br/>

![React](https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-5-646CFF?style=for-the-badge&logo=vite&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?style=for-the-badge&logo=mongodb&logoColor=white)
![Razorpay](https://img.shields.io/badge/Razorpay-Payments-072654?style=for-the-badge&logo=razorpay&logoColor=white)
![Tailwind](https://img.shields.io/badge/Tailwind_CSS-3-38B2AC?style=for-the-badge&logo=tailwindcss&logoColor=white)

<br/>

[Features](#-features) · [Tech Stack](#-tech-stack) · [Getting Started](#-getting-started) · [Docker](#-running-with-docker) · [API](#-api-endpoints) · [Project Structure](#-project-structure)

</div>

---

## ✨ Features

| Area | What you get |
|------|----------------|
| 🔍 **Smart search** | Search buses by source, destination, and journey date |
| 🪑 **Seat selection** | Interactive seat layout with real-time selection |
| 👤 **Auth** | Sign up / login with JWT-protected routes |
| 💳 **Payments** | Razorpay checkout with server-side payment verification |
| 🎫 **Bookings** | View booking history under *My Bookings* |
| 📱 **Responsive UI** | Works smoothly on desktop and mobile |

---

## 🛠 Tech Stack

<table>
<tr>
<td width="50%" valign="top">

### Frontend (`client/`)
- **React 18** + **TypeScript**
- **Vite** — fast dev server & builds
- **Tailwind CSS** — utility-first styling
- **React Router** — client routing
- **Axios / Fetch** — API calls
- **React Hot Toast** — notifications
- **Lucide React** — icons

</td>
<td width="50%" valign="top">

### Backend (`server/`)
- **Node.js** + **Express**
- **MongoDB** + **Mongoose**
- **JWT** — authentication
- **bcryptjs** — password hashing
- **Razorpay** — payment orders & verify
- **CORS** — cross-origin support
- **dotenv** — environment config

</td>
</tr>
</table>

---

## 🚀 Getting Started

### Prerequisites

- Node.js **18+**
- npm or yarn
- MongoDB Atlas (or local MongoDB)
- Razorpay test keys ([dashboard.razorpay.com](https://dashboard.razorpay.com))

### 1. Clone the repository

```bash
git clone https://github.com/ayushdhiman7/red-bus.git
cd red-bus
```

### 2. Backend setup

```bash
cd server
npm install
```

Create a `server/.env` file:

```env
MONGO_URI=your_mongodb_connection_string
NODE_ENV=development
JWT_SECRET=your_jwt_secret
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
PORT=5000
```

Start the API:

```bash
npm run dev
```

Server runs at **http://localhost:5000**

### 3. Frontend setup

```bash
cd client
npm install
```

Create a `client/.env` file:

```env
VITE_API_URL=http://localhost:5000
REACT_APP_RAZORPAY_KEY=your_razorpay_key_id
```

Start the UI:

```bash
npm run dev
```

App runs at **http://localhost:5173**

> **Tip:** Open DevTools → Network to inspect API calls while developing locally.

---

## 🐳 Running with Docker

Run the full stack (frontend + backend) in containers with live code sync for development.

### Prerequisites

- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/)
- MongoDB Atlas connection string (or uncomment the `mongodb` service in `docker-compose.yml` for a local database)
- Razorpay test keys

### 1. Configure environment files

Create the same `.env` files as in [Getting Started](#-getting-started):

**`server/.env`**

```env
MONGO_URI=your_mongodb_connection_string
NODE_ENV=development
JWT_SECRET=your_jwt_secret
RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
PORT=5000
```

**`client/.env`**

```env
VITE_API_URL=http://localhost:5000
REACT_APP_RAZORPAY_KEY=your_razorpay_key_id
```

> **Important:** Use `http://localhost:5000` for `VITE_API_URL` when running locally with Docker. The browser runs on your host machine, so it must reach the backend via the published port — not the internal Docker service name (`backend`).

### 2. Build and start

From the project root:

```bash
docker compose build
docker compose up
```

| Service   | URL                         |
|-----------|-----------------------------|
| Frontend  | http://localhost:5173       |
| Backend   | http://localhost:5000       |

Stop the stack:

```bash
docker compose down
```

### How it works

- **`docker-compose.yml`** defines two services: `frontend` (Vite) and `backend` (Express).
- **Volume mounts** sync `./client` and `./server` into the containers so code changes reflect immediately without rebuilding.
- **Anonymous volumes** for `/app/node_modules` keep container dependencies separate from your host.
- **Vite** is configured with `host: true` in `client/vite.config.ts` so the dev server is reachable from outside the container (required for port mapping to work).

### Useful commands

```bash
# Rebuild images after dependency changes
docker compose build

# Run in detached (background) mode
docker compose up -d

# View logs
docker compose logs -f

# Restart a single service
docker compose restart frontend
```

---

## 📡 API Endpoints

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| `POST` | `/api/auth/signup` | ❌ | Register a new user |
| `POST` | `/api/auth/login` | ❌ | Login and receive JWT |
| `GET` | `/api/auth/user` | ✅ | Get current user profile |
| `POST` | `/api/create-order` | ✅ | Create Razorpay order & booking |
| `POST` | `/api/verify-payment` | ✅ | Verify payment signature |

Pass the token as:

```http
Authorization: Bearer <jwt_token>
```

---

## 📁 Project Structure

```
red-bus/
├── client/                 # React + Vite frontend
│   ├── src/
│   │   ├── components/     # UI components (layout, booking, search)
│   │   ├── contexts/       # Auth & booking state
│   │   ├── pages/          # Route screens
│   │   ├── services/       # API helpers
│   │   ├── data/           # Mock / static data
│   │   └── types/          # TypeScript types
│   ├── Dockerfile          # Frontend container image
│   ├── .env                # Frontend env (gitignored)
│   └── package.json
│
├── server/                 # Express + MongoDB API
│   ├── src/                # Models, controllers, middleware
│   ├── server.js           # App entry point
│   ├── Dockerfile          # Backend container image
│   ├── .env                # Backend env (gitignored)
│   └── package.json
│
├── docker-compose.yml      # Multi-container orchestration
├── data/                   # Sample JSON datasets
└── README.md
```

---

## 🔐 Environment Notes

- Never commit `.env` files — they are ignored by `.gitignore`
- Use **Razorpay test mode** keys while developing
- Rotate secrets if they were ever pushed to a remote

---

## 🖥 User Flow

```text
Home → Search buses → Bus details → Select seats
     → Login (if needed) → Checkout → Razorpay payment
     → Payment success → My Bookings
```

---

## 📜 License

```
Copyright © 2026 Ayush Dhiman
All Rights Reserved.
```

Unauthorized copying, distribution, or modification of this project,
via any medium, is strictly prohibited without prior written permission
from the author.

---

<div align="center">

**Made with ❤️ by Ayush Dhiman**

*All Rights Reserved by Ayush Dhiman*

</div>
