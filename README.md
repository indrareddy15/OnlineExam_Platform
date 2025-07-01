# Online Exam Platform

A robust, full-stack web application for conducting secure, scalable online examinations. The platform supports real-time exam delivery, automated evaluation, comprehensive analytics, and fine-grained role-based access control (RBAC).

---

## 🌟 Key Features

### User Management

- **Multi-Role Access**: Student, Instructor, and Admin roles, each with specific permissions.
- **Secure Authentication**: JWT-based authentication with refresh token system.
- **Profile Management**: Customizable user profiles and account activation/deactivation.
- **Account Security**: Passwords hashed with bcrypt, session and violation tracking.

### Question Bank

- **Flexible Question Types**: Supports single/multiple choice, true/false, short answer, and essay questions.
- **Organization and Analytics**: Categorization, tagging, difficulty levels, and usage metrics.
- **Bulk Operations**: Import/export and batch management for questions.

### Exam Management

- **Scheduling and Settings**: Flexible exam start/end times, duration, shuffling, retake policies, automatic submission.
- **Participant Control**: Enrollment management and access restrictions.
- **Proctoring**: Real-time violation detection and monitoring. ***Not implemented***

### Real-Time Exam Delivery

- **Live Sessions**: Powered by Socket.IO for synchronized exam experiences. ***Not implemented***
- **Session Management**: Auto-save, persistent state, timer synchronization, navigation tracking.
- **Security Monitoring**: Detection of tab switches, full-screen exits, and browser activity with violation logging.

### Results & Analytics

- **Automated Evaluation**: Instant scoring for objective questions.
- **Comprehensive Reporting**: Individual and class analytics, grade distributions, time analysis, and ranking.
- **Export Options**: Results can be exported in various formats. ***Not implemented***

### Notification System

- **Multi-Channel Alerts**: Email and in-app notifications for exam reminders and results. ***Not implemented***
- **Prioritization & Scheduling**: Urgent and scheduled notifications.***Not implemented***

### Security

- **RBAC**: Enforced role-based access control on all endpoints.
- **Input Validation & Rate Limiting**: Comprehensive validation using Joi, and protection from brute force.
- **CORS & Security Headers**: Configured via CORS and Helmet.js.
- **Sensitive Data Encryption**: All sensitive information is securely encrypted.

### Performance & Monitoring

- **Efficient Querying**: Indexed MongoDB queries and caching for high performance.
- **Real-Time Updates**: Live exam status and notifications using Socket.IO.
- **Logging**: Winston-based logging with error, warning, info, and debug levels.
- **Audit Logging**: Secure tracking of critical system events.

---

## 🏗️ System Architecture

### Backend (Node.js/Express)

```
src/
├── config/               # App configuration
├── middleware/           # Express middlewares (auth, role checks)
├── models/               # Mongoose schemas (User, Exam, Question, etc.)
├── routes/               # Express route handlers
├── services/             # Business logic
├── utils/                # Utility modules
└── index.js              # Application entry point
```

### Frontend (React/TypeScript)

```
src/
├── components/           # Reusable UI components
├── contexts/             # React context providers
├── pages/                # Application pages (auth, dashboard, exams, etc.)
├── services/             # API service layer
└── App.tsx               # Main app component
```

---

## 🛠️ Technology Stack

### Backend

- **Node.js** with **Express.js**
- **MongoDB** via **Mongoose ODM**
- **JWT** authentication with refresh tokens
- **Socket.IO** for real-time communication
- **Nodemailer** for emails
- **Joi** for validation
- **Jest** & **Supertest** for testing
- **Winston** for logging
- **node-cron** for scheduled tasks
- **Security**: Helmet, CORS, rate limiting

### Frontend

- **React 18** with **TypeScript**
- **Vite** build tool
- **Tailwind CSS** for styling
- **React Router DOM v6** for routing
- **React Context API** for state management
- **Lucide React** for icons

---

#### Test Accounts (Seeded)

- **Admin**: admin@oec.com / admin123
- **Instructor**: instructor@oec.com / instructor123
- **Students**: student1@oec.com ... student5@oec.com / student123

---

## 📡 API Overview

### Authentication

- `POST /api/users/register` – Register a new user
- `POST /api/users/login` – Login
- `POST /api/users/refresh-token` – Refresh JWT
- `POST /api/users/logout` – Logout

### Exams

- `POST /api/exams` – Create exam (Instructor/Admin)
- `GET /api/exams` – List exams
- `GET /api/exams/:id` – Get exam details
- `PUT /api/exams/:id` – Update exam
- `DELETE /api/exams/:id` – Delete exam

### Exam Delivery

- `GET /api/exam-delivery/:examId/start` – Start exam session
- `POST /api/exam-delivery/:sessionId/answer` – Submit answer
- `POST /api/exam-delivery/:sessionId/submit` – Submit completed exam

### Questions

- `POST /api/questions` – Create question
- `GET /api/questions` – List questions
- `GET /api/questions/:id` – Get question details
- `PUT /api/questions/:id` – Update question
- `DELETE /api/questions/:id` – Delete question

### Results

- `POST /api/results/submit` – Submit results (Student)
- `GET /api/results/exam/:examId` – Get exam results (Instructor/Admin)
- `GET /api/results/:userId` – Get user results

---


## 📈 Performance & Real-time Features

- **Optimized Queries**: Indexed and cached MongoDB queries for speed.
- **Live Exam Sessions**: Real-time experience for exam takers and invigilators.
- **Instant Notifications**: Push alerts for important events.
- **Session Synchronization**: Users can resume interrupted sessions. ***Not Implemented***
- **Live Monitoring**: Real-time tracking of exam activity and violations. ***Not Implemented***
- **Automatic Updates**: Real-time status and result updates.

---

## 📱 Responsive & Accessible Design

- **Mobile-First**: Optimized for mobile and desktop devices.
- **Responsive Layout**: Adapts to all screen sizes.
- **Touch & Cross-Browser Friendly**: Works on all modern browsers.
- **Accessibility**: Designed to meet WCAG 2.1 guidelines.

---

## 🛡️ Security Highlights

- **JWT & Refresh Tokens**: Secure, stateless authentication flow.
- **RBAC**: Strict role-based access applied to all APIs and routes.
- **Input Validation**: Joi schemas throughout.
- **Rate Limiting**: Prevents brute-force and abuse.
- **CORS & Helmet**: Protects from common web vulnerabilities.
- **Password Hashing**: Bcrypt with configurable rounds.
- **Audit Logging**: Tracks sensitive actions.***Not Implemented***

---

## 🗂️ Database Models (Sample)

### User

```javascript
{
  name: String,
  email: String (unique),
  password: String (hashed),
  role: Enum ['student', 'instructor', 'admin'],
  refreshTokens: Array,
  profile: Object,
  isActive: Boolean,
  lastLogin: Date,
  createdAt: Date,
  updatedAt: Date
}
```

### Exam

```javascript
{
  title: String,
  description: String,
  startTime: Date,
  endTime: Date,
  duration: Number,
  questions: Array,
  settings: Object,
  participants: Array,
  isActive: Boolean,
  isPublished: Boolean
}
```

### Question

```javascript
{
  text: String,
  type: Enum ['single-choice', 'multiple-choice', 'true-false', 'short-answer', 'essay'],
  options: Array,
  correctAnswer: String,
  marks: Number,
  difficulty: Enum ['easy', 'medium', 'hard'],
  category: String,
  tags: Array
}
```

---

## 🗳️ Role Matrix

| Feature                 | Student     | Instructor     | Admin     |
|------------------------|-------------|---------------|-----------|
| Profile Management     | ✅ Own      | ✅ Own        | ✅ All    |
| Exam Taking            | ✅ Assigned | ✅ All        | ✅ All    |
| Exam Creation          | ❌          | ✅ Own        | ✅ All    |
| Question Management    | ❌          | ✅ Own        | ✅ All    |
| Results Viewing        | ✅ Own      | ✅ Own Exams  | ✅ All    |
| Analytics              | ✅ Personal | ✅ Own Exams  | ✅ System |
| User Management        | ❌          | ❌           | ✅ All    |
| System Settings        | ❌          | ❌           | ✅ All    |
| Notifications          | ✅ Receive  | ✅ Send/Manage| ✅ All    |

---

## 👥 Authors & Acknowledgments

- **Ganta Indra Reddy** – Initial work and ongoing maintenance

## 🎯 Project Status

**Production Ready:** Only few featured and deployable, soon will update the all real time features.

---

## Further Reading

***Will Add Soon***
