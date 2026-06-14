# WebRTC Video Meeting Application

## Overview
This project is a WebRTC-based video meeting application built with React on the frontend and Node.js + Express + Socket.IO on the backend. It supports real-time video/audio calls, chat messaging, user authentication, and meeting history.

## Project Structure
- `Backend/` — Node.js server, Socket.IO signaling, REST API, MongoDB models
- `Frontend/` — React SPA, routing, authentication, WebRTC meeting UI

## System Architecture
The system has three main parts:
1. Browser client (React app)
2. Backend server (Express + Socket.IO)
3. Database (MongoDB Atlas)

### How it works
- User authenticates with a username/password
- User opens a meeting URL to join a room
- Frontend requests camera/microphone permissions
- Browser obtains local media stream and connects to Socket.IO server
- Backend groups room users by URL path and forwards signaling messages
- Clients exchange SDP offers/answers and ICE candidates
- WebRTC peer connections are established for video/audio
- Chat messages are relayed through Socket.IO
- Meeting history is stored in MongoDB for each authenticated user

## Features
- Real-time video conferencing with multiple participants
- Audio on/off and video on/off toggles
- Screen sharing support
- In-call text chat
- User sign-up and login
- Meeting history tracking

## Backend Components
- `Backend/app.js` — application entry point
- `Backend/src/controllers/socketManager.js` — Socket.IO connection and signaling logic
- `Backend/src/controllers/user.controller.js` — login, registration, history endpoints
- `Backend/src/models/user.model.js` — user schema
- `Backend/src/models/meeting.model.js` — meeting history schema
- `Backend/src/routes/users.routes.js` — REST routes for auth and history

## Frontend Components
- `Frontend/src/App.js` — React routes and main app shell
- `Frontend/src/pages/VideoMeet.jsx` — WebRTC conference logic and UI
- `Frontend/src/pages/authentication.jsx` — login/register UI
- `Frontend/src/contexts/AuthContext.jsx` — auth API and user state management
- `Frontend/src/utils/withAuth.jsx` — protected route wrapper
- `Frontend/src/environment.js` — backend server endpoint configuration

## Libraries Used and Why
### Frontend
- `react`, `react-dom` — core UI framework
- `react-router-dom` — page routing and dynamic meeting URLs
- `axios` — HTTP client for backend API calls
- `socket.io-client` — real-time signaling for WebRTC
- `@mui/material`, `@mui/icons-material` — UI components and icons
- `@emotion/react`, `@emotion/styled` — styling support for MUI
- `http-status` — readable HTTP status codes
- `react-transition-group` — animation support (UI transitions)
- `web-vitals` — performance measurement utilities

### Backend
- `express` — web server and REST API framework
- `socket.io` — real-time bidirectional server-client communication
- `mongoose` — MongoDB object modeling and schema enforcement
- `bcrypt` — secure password hashing
- `cors` — enable frontend-backend cross-origin requests
- `http-status` — standardized HTTP status codes

## Data Model
### User
- `name`
- `username`
- `password` (hashed)
- `token`

### Meeting
- `user_id`
- `meetingCode`
- `date`

## Notes and Recommendations
- The backend currently includes an extra `soket.io` dependency that appears to be a typo and can be removed.
- Chat history is stored in server memory only, so it is not persistent across restarts.
- The current MongoDB connection string is hardcoded in `Backend/app.js`; it should be moved to environment variables for production.
- User tokens do not currently expire, so token lifecycle management should be improved for security.

## Running the Project
### Backend
1. Open `Backend/`
2. Install dependencies: `npm install`
3. Run server: `npm run dev`

### Frontend
1. Open `Frontend/`
2. Install dependencies: `npm install`
3. Run app: `npm start`

## Conclusion
This project demonstrates a full-stack WebRTC meeting solution with authentication, signaling, chat, and history tracking. It combines React UI, Socket.IO real-time signaling, and MongoDB storage to deliver a collaborative meeting experience.
