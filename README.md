# DevTinder

A full-stack web application that facilitates professional connections between developers. Inspired by networking needs in the tech community, DevTinder allows developers to discover, match, and collaborate with peers based on shared skills, tech stacks, and project interests.

## 📋 Project Overview

DevTinder is a modern networking platform designed specifically for developers to find and connect with other developers. Think of it as "Tinder for Devs" - users can browse through developer profiles, express interest, and build meaningful professional connections. The platform features real-time chat, premium subscriptions, and an intelligent matching system.

## 🏗️ Architecture

This project consists of two main components:

### Backend (`devTinder-main/`)
A robust Node.js/Express REST API server that handles:
- User authentication and authorization
- Profile management
- Connection requests and matching logic
- Real-time messaging via Socket.io
- Payment processing with Razorpay
- Email notifications via AWS SES
- Automated cron jobs for maintenance tasks

### Frontend (`devTinder-web-main/`)
A responsive React-based single-page application featuring:
- Modern UI built with React 18 and Vite
- State management using Redux Toolkit
- Styled with TailwindCSS and DaisyUI
- Real-time chat interface
- Profile browsing and matching interface

## ✨ Key Features

### 🔐 Authentication & Authorization
- Secure user registration and login
- JWT-based authentication
- Password encryption with bcrypt
- Cookie-based session management

### 👤 User Profiles
- Comprehensive developer profiles with skills, experience, and interests
- Profile editing and customization
- Profile photo support
- Age and gender preferences

### 🤝 Connection System
- Swipe-style feed to browse other developers
- Send connection requests (interested/ignored)
- Accept or reject incoming requests
- View all active connections
- Smart feed algorithm that excludes already-connected users

### 💬 Real-Time Chat
- Live messaging with Socket.io
- One-on-one conversations with connections
- Instant message delivery and notifications
- Chat history persistence

### 💳 Premium Features
- Subscription-based premium access
- Razorpay payment integration
- Enhanced profile visibility for premium users
- Access to advanced features

### 📧 Email Notifications
- AWS SES integration for transactional emails
- Connection request notifications
- Password reset functionality
- System updates and announcements

### ⚙️ Background Jobs
- Automated cron jobs for data cleanup
- Scheduled maintenance tasks
- Database optimization

## 🛠️ Technology Stack

### Backend Technologies
- **Runtime:** Node.js
- **Framework:** Express.js
- **Database:** MongoDB with Mongoose ODM
- **Authentication:** JWT (jsonwebtoken), bcrypt
- **Real-time:** Socket.io
- **Payment:** Razorpay
- **Email:** AWS SES (@aws-sdk/client-ses)
- **Validation:** validator.js
- **Scheduling:** node-cron
- **Security:** CORS, cookie-parser

### Frontend Technologies
- **Framework:** React 18
- **Build Tool:** Vite
- **State Management:** Redux Toolkit
- **Routing:** React Router v6
- **Styling:** TailwindCSS, DaisyUI
- **HTTP Client:** Axios
- **Real-time:** Socket.io-client

## 📂 Project Structure

```
devTinder-main/              # Backend API
├── src/
│   ├── app.js              # Main application entry point
│   ├── config/
│   │   └── database.js     # MongoDB connection setup
│   ├── middlewares/
│   │   └── auth.js         # Authentication middleware
│   ├── models/
│   │   ├── user.js         # User schema and model
│   │   ├── connectionRequest.js  # Connection request schema
│   │   ├── chat.js         # Chat message schema
│   │   └── payment.js      # Payment transaction schema
│   ├── routes/
│   │   ├── auth.js         # Authentication routes (signup, login, logout)
│   │   ├── profile.js      # Profile management routes
│   │   ├── request.js      # Connection request routes
│   │   ├── user.js         # User discovery and connections
│   │   ├── chat.js         # Chat routes
│   │   └── payment.js      # Payment processing routes
│   └── utils/
│       ├── validation.js   # Input validation helpers
│       ├── socket.js       # Socket.io configuration
│       ├── razorpay.js     # Razorpay integration
│       ├── sesClient.js    # AWS SES email client
│       ├── sendEmail.js    # Email sending utilities
│       ├── cronjob.js      # Scheduled tasks
│       └── constants.js    # Application constants

devTinder-web-main/          # Frontend React App
├── src/
│   ├── App.jsx             # Main app component with routing
│   ├── main.jsx            # Application entry point
│   ├── components/
│   │   ├── Body.jsx        # Main layout wrapper
│   │   ├── NavBar.jsx      # Navigation component
│   │   ├── Footer.jsx      # Footer component
│   │   ├── Login.jsx       # Login/Signup page
│   │   ├── Feed.jsx        # Developer feed/swipe interface
│   │   ├── Profile.jsx     # User profile page
│   │   ├── EditProfile.jsx # Profile editing interface
│   │   ├── Connections.jsx # List of connections
│   │   ├── Requests.jsx    # Pending connection requests
│   │   ├── Chat.jsx        # Real-time chat interface
│   │   ├── Premium.jsx     # Premium subscription page
│   │   └── UserCard.jsx    # Developer profile card component
│   └── utils/
│       ├── appStore.js     # Redux store configuration
│       ├── userSlice.js    # User state management
│       ├── feedSlice.js    # Feed state management
│       ├── connectionSlice.js  # Connections state
│       ├── requestSlice.js # Requests state
│       ├── socket.js       # Socket.io client setup
│       └── constants.js    # Frontend constants
└── public/                 # Static assets
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local or Atlas)
- npm or yarn package manager

### Backend Setup

1. Navigate to the backend directory:
```bash
cd devTinder-main
```

2. Install dependencies:
```bash
npm install
```

3. Create a `.env` file with the following variables:
```env
PORT=7777
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
RAZORPAY_KEY_ID=your_razorpay_key
RAZORPAY_KEY_SECRET=your_razorpay_secret
AWS_REGION=your_aws_region
AWS_ACCESS_KEY_ID=your_aws_access_key
AWS_SECRET_ACCESS_KEY=your_aws_secret_key
```

4. Start the development server:
```bash
npm run dev
```

The API server will run on `http://localhost:7777`

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd devTinder-web-main
```

2. Install dependencies:
```bash
npm install
```

3. Start the development server:
```bash
npm run dev
```

The React app will run on `http://localhost:5173`

## 🔌 API Endpoints

### Authentication
- `POST /signup` - Register a new user
- `POST /login` - User login
- `POST /logout` - User logout

### Profile Management
- `GET /profile/view` - View user profile
- `PATCH /profile/edit` - Update profile information
- `PATCH /profile/password` - Reset/change password

### Connection Requests
- `POST /request/send/:status/:userId` - Send connection request (interested/ignored)
- `POST /request/review/:status/:requestId` - Accept/reject connection request

### User Discovery
- `GET /user/feed` - Get feed of potential connections
- `GET /user/requests/received` - View pending requests
- `GET /user/connections` - View all connections

### Chat
- Real-time messaging via Socket.io
- Chat history retrieval endpoints

### Payments
- Premium subscription endpoints
- Payment verification and processing

## 🎯 Core Workflows

### User Registration & Login
1. User signs up with email, password, and profile details
2. Password is hashed and stored securely
3. JWT token is generated and sent as HTTP-only cookie
4. User is redirected to feed

### Connection Flow
1. User browses through developer profiles in the feed
2. User can express interest or ignore each profile
3. If both users express interest, a connection is established
4. Connected users can chat in real-time

### Chat System
1. Socket.io establishes WebSocket connection
2. Messages are sent in real-time between connected users
3. Chat history is persisted in MongoDB
4. Typing indicators and online status

### Premium Subscription
1. User initiates payment through Razorpay
2. Payment is verified on the backend
3. User account is upgraded to premium
4. Enhanced features are unlocked

## 🔒 Security Features

- Password hashing with bcrypt (10 salt rounds)
- JWT token-based authentication
- HTTP-only cookies to prevent XSS attacks
- CORS configuration for cross-origin security
- Input validation using validator.js
- Strong password requirements
- Protected API routes with authentication middleware

## 🎨 UI/UX Highlights

- Responsive design for all device sizes
- Swipe-style card interface for browsing profiles
- Real-time updates and notifications
- Clean, modern design with DaisyUI components
- Smooth animations and transitions
- Intuitive navigation and user flow

## 📱 Routes & Pages

- `/` - Main feed (requires authentication)
- `/login` - Login/Signup page
- `/profile` - User profile view
- `/connections` - List of all connections
- `/requests` - Pending connection requests
- `/premium` - Premium subscription page
- `/chat/:targetUserId` - Chat with a specific user

## 🧪 Development

### Backend Development
```bash
npm run dev  # Runs with nodemon for auto-reload
```

### Frontend Development
```bash
npm run dev  # Runs Vite dev server with HMR
```

### Building for Production
```bash
# Frontend
npm run build
npm run preview  # Preview production build

# Backend
npm start  # Production server
```

## 👥 Author

**Akshay Saini**

## 📄 License

ISC

## 🤝 Contributing

This project is part of a learning initiative. Feel free to fork and experiment with the code!

---

**DevTinder** - Connecting developers, one match at a time! 👨‍💻💙👩‍💻
