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
- **Dotenv** for environment variables

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
 ###⚙️ Installation & Setup
###1️⃣ Clone the Repository
```git clone https://github.com/your-username/uber-clone.git
cd uber-clone


