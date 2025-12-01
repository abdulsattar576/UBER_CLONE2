# Uber Clone 🚖 (MERN + Maps + Socket.io)

A full-stack ride-hailing application built with the **MERN stack**, integrating **real-time location updates** and **live ride status** using **Socket.io** and a **Maps API** (e.g., Google Maps / Mapbox).  
This project mimics core features of apps like Uber: ride requests, driver matching, live tracking, and fare estimation.

---

## 🧾 Features

### 👤 Authentication & Users
- JWT-based **user and driver authentication**
- Separate flows for **Rider** and **Driver**
- Secure password hashing using **bcrypt**
- Protected routes on both frontend and backend

### 🚕 Ride Management
- Rider can:
  - Set **pickup** and **dropoff** locations using the map
  - See **route preview** and **estimated fare**
  - Request a ride and see **driver search status**
- Driver can:
  - Go **online / offline**
  - See nearby ride requests
  - **Accept / reject** ride requests

### 🗺️ Maps & Location
- Integrated **Maps API** (e.g., Google Maps / Mapbox)
- Search locations using **autocomplete**
- Show **pickup and destination markers**
- Show **route polyline** between points
- Live **driver location tracking** on map

### ⚡ Real-Time (Socket.io)
- Real-time **ride request notifications**
- Real-time **ride acceptance / cancellation**
- Real-time **driver location updates** (simulated or from device)
- Real-time **ride status** (Searching, Accepted, On Trip, Completed)

### 💳 Payments (Optional / Demo)
- Static / mock fare calculation based on **distance & duration**
- (Optional) Integration with real payment gateway (Stripe, etc.)

---

## 🛠️ Tech Stack

### Frontend
- **React.js**
- **Redux / Context API** (state management)
- **Axios** for API calls
- **Socket.io Client**
- **Maps JavaScript SDK** (Google Maps / Mapbox GL JS)
- **Tailwind CSS / Material UI / Custom CSS** for UI

### Backend
- **Node.js** + **Express.js**
- **MongoDB** + **Mongoose**
- **Socket.io** for real-time communication
- **JSON Web Tokens (JWT)** for auth
- **bcrypt** for password hashing
- **dotenv** for environment variables

---

## 📁 Project Structure

```bash
uber-clone/
├── backend/
│   ├── src/
│   │   ├── config/        # DB & config files
│   │   ├── controllers/   # Auth, Ride, User, Driver controllers
│   │   ├── models/        # Mongoose models (User, Driver, Ride)
│   │   ├── routes/        # Express routes
│   │   ├── sockets/       # Socket.io events (ride, location)
│   │   ├── middlewares/   # Auth middleware
│   │   └── server.js      # Entry point
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── api/           # Axios instances / API calls
│   │   ├── components/    # Reusable UI components
│   │   ├── context/ or store/ # Global state (Redux/Context)
│   │   ├── pages/         # Main pages (Login, Home, Ride, Driver)
│   │   └── App.jsx
│   └── package.json
│
└── README.md
```

---

## 🚀 Getting Started

### ✅ Prerequisites

Make sure you have:

- **Node.js** (LTS)
- **npm** or **yarn**
- **MongoDB** (local or MongoDB Atlas)
- A **Maps API key** (e.g., Google Maps JS API / Mapbox)

---

## 🧩 Backend Setup

Go to the backend folder:

```bash
cd backend
```

Install backend dependencies:

```bash
npm install
```

Create a `.env` file in the `backend` directory (same level as `package.json`):

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
CLIENT_URL=http://localhost:3000
```

- `MONGO_URI`: Your MongoDB / MongoDB Atlas connection string  
- `JWT_SECRET`: Any strong random string (used to sign JWT tokens)  
- `CLIENT_URL`: URL of your frontend app in development  

Start the backend server:

```bash
npm run dev
```

Or:

```bash
npm start
```

By default, backend will run at:

```text
http://localhost:5000
```

---

## 🧩 Frontend Setup

Open a new terminal and go back to the project root (if not already):

```bash
cd uber-clone
```

Go to the frontend folder:

```bash
cd frontend
```

Install frontend dependencies:

```bash
npm install
```

Create a `.env` file in the `frontend` directory (for Vite-style env vars; adjust if using CRA):

```env
VITE_API_BASE_URL=http://localhost:5000
VITE_SOCKET_URL=http://localhost:5000
VITE_MAPS_API_KEY=your_maps_api_key
```

- `VITE_API_BASE_URL`: URL of your backend API  
- `VITE_SOCKET_URL`: URL of your Socket.io server (usually same as backend)  
- `VITE_MAPS_API_KEY`: Your Google Maps / Mapbox API key  

Start the frontend dev server:

```bash
npm run dev
```

The app will be available at:

```text
http://localhost:3000
```

---

## ▶️ Run the App

Make sure **both** are running:

- Backend: `http://localhost:5000`
- Frontend: `http://localhost:3000`

Open the frontend URL in your browser and:

- Register/login as **Rider** to request rides  
- Register/login as **Driver** to accept rides and test real-time features  

---

## 📜 Project Scripts

### Backend (`/backend`)

```bash
npm run dev     # Start backend in development (with nodemon)
npm start       # Start backend in production mode
```

### Frontend (`/frontend`)

```bash
npm run dev     # Start frontend dev server
npm run build   # Build for production
npm run preview # Preview production build (Vite)
```

---

## 🔑 Environment Variables

### Backend `.env`

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
CLIENT_URL=http://localhost:3000
```

> Add any other keys like `GOOGLE_MAPS_API_KEY` if you call Maps API from backend.

### Frontend `.env`

```env
VITE_API_BASE_URL=http://localhost:5000
VITE_SOCKET_URL=http://localhost:5000
VITE_MAPS_API_KEY=your_maps_api_key
```

> For Create React App, you can instead use:  
> `REACT_APP_API_URL`, `REACT_APP_SOCKET_URL`, etc.

---

## 🌐 Socket.io Events

Here’s a high-level overview of the WebSocket events between client and server.

### Rider → Server

#### `ride:request`

Emitted when a rider requests a ride.

**Payload example:**

```json
{
  "riderId": "string",
  "pickup": "Pickup address",
  "destination": "Destination address",
  "pickupCoords": { "lat": 0, "lng": 0 },
  "destinationCoords": { "lat": 0, "lng": 0 },
  "fareEstimate": 250
}
```

#### `ride:cancel`

Rider cancels request before driver accepts.

---

### Driver → Server

#### `driver:online`

Driver comes online & shares current location.

#### `driver:offline`

Driver goes offline.

#### `ride:accept`

Driver accepts a ride.

**Payload example:**

```json
{
  "rideId": "string",
  "driverId": "string"
}
```

#### `location:update`

Driver sends updated GPS position.

**Payload example:**

```json
{
  "rideId": "string",
  "driverId": "string",
  "coords": { "lat": 0, "lng": 0 }
}
```

---

### Server → Clients

- `ride:new` – Server broadcasts a new ride request to nearby online drivers.  
- `ride:accepted` – Sent to rider when a driver accepts.  
- `ride:updated` – Status updates (on the way, arrived, on trip, completed).  
- `ride:completed` – Sent to rider and driver when ride is finished.  

---

## 🧮 Ride & Fare Logic

Example fare calculation formula:

```text
totalFare = baseFare + (perKmRate * distanceInKm) + (perMinuteRate * durationInMinutes)
```

- **Distance & duration**: Retrieved from Maps API Directions endpoint (e.g., Google Directions API).  
- **Rates**: Configurable in backend (e.g., a `config` file or DB collection).

You can extend this with:

- Surge pricing  
- Minimum fare  
- Cancellation charges  

---

## 🖼️ Screenshots

Main UI Preview:

<img width="1920" height="1080" alt="Uber Clone UI" src="https://github.com/user-attachments/assets/b65e404e-665c-467a-ab09-ad68d9527fa3" />

---

## 🔐 Security & Best Practices

- Never commit `.env` files or API keys (use `.gitignore`).  
- Use **HTTPS** in production.  
- Validate and sanitize all request bodies on backend.  
- Use **CORS** and limit allowed origins to your frontend URL.  
- Store **JWT** securely (e.g., HttpOnly cookies or careful `localStorage` usage).  
- Set reasonable **JWT expiry times** and consider refresh tokens.  
- Add **rate limiting** & **brute-force protection** on auth routes (e.g., `express-rate-limit`).  

---

## 🌍 Deployment Guide

You can deploy this stack using:

### Frontend

- **Vercel**, **Netlify**, or any static hosting provider

Build command:

```bash
npm run build
```

### Backend

- **Render**, **Railway**, **VPS (DigitalOcean, AWS EC2, etc.)**, etc.

Make sure to:

- Set environment variables in the hosting dashboard  
- Enable WebSockets / long-lived connections  
- Configure CORS for your production frontend URL  

### Database

- **MongoDB Atlas** (recommended)  
  Use the Atlas connection string in `MONGO_URI`.

### Important

Update frontend `.env` in production:

```env
VITE_API_BASE_URL=https://your-backend-domain.com
VITE_SOCKET_URL=https://your-backend-domain.com
```

On backend, set:

```env
CLIENT_URL=https://your-frontend-domain.com
```

Ensure CORS & Socket.io CORS allow the deployed frontend origin.

---

## 🧭 Future Improvements

Some ideas to enhance this project:

- 📱 Mobile App using React Native  
- 💸 Real payment integration (Stripe, PayPal, etc.)  
- ⭐ Ratings & reviews for drivers and riders  
- 💬 In-app chat between rider & driver  
- 🔔 Push notifications (Firebase Cloud Messaging / OneSignal)  
- 📊 Admin dashboard for monitoring rides, users, and drivers  
- 📈 Analytics (total trips, revenue, active drivers, etc.)  

---

## 👨‍💻 Author

**Abdul Sattar**  
_MERN Stack / Web & Mobile Developer_

- GitHub: `https://github.com/abdulsattar576`  
- LinkedIn: `https://www.linkedin.com/in/abdul-sattar-se/`  
- Email: `sattargkl4@gmail.com`  

> Feel free to fork this project, open issues, or submit pull requests.

---

## 📄 License

This project is licensed under the **MIT License**.  
You are free to use, modify, and distribute it with attribution.
