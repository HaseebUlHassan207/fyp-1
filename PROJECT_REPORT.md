# CRS - Curriculum Resource System
## Comprehensive Project Report

**Project Date:** December 15, 2025  
**Repository Owner:** abrauf18  
**Current Branch:** main  
**Report Type:** Complete Architecture & Features Analysis

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Project Overview](#project-overview)
3. [Technology Stack](#technology-stack)
4. [Architecture Overview](#architecture-overview)
5. [Core Features & Modules](#core-features--modules)
6. [Database Schema](#database-schema)
7. [API Endpoints & Routes](#api-endpoints--routes)
8. [User Roles & Access Control](#user-roles--access-control)
9. [Frontend Implementation](#frontend-implementation)
10. [Key Technical Implementations](#key-technical-implementations)
11. [Deployment & Configuration](#deployment--configuration)
12. [Conclusion](#conclusion)

---

## Executive Summary

CRS (Curriculum Resource System) is a comprehensive, full-stack learning management system designed to streamline curriculum delivery and resource management. The system supports multiple user roles including students, teachers, schools, and administrators, with sophisticated features for managing educational content, classrooms, assessments, and student progress tracking.

The application is built with a modern technology stack using Next.js for the frontend and Express.js with Sequelize ORM for the backend, with PostgreSQL as the primary database. The system demonstrates enterprise-grade architecture with role-based access control, secure authentication, and robust data management capabilities.

---

## Project Overview

### Mission & Purpose

CRS is designed to:
- Enable schools to create and manage learning standards and curriculum
- Allow teachers to organize classrooms, assign resources, and track student progress
- Provide students with personalized learning experiences
- Facilitate resource sharing across multiple educational resource types
- Track student engagement and performance metrics
- Manage school billing and payment processing

### Project Scope

The project consists of two main components:
1. **Frontend (crs/)**: A Next.js 14 application with TypeScript support
2. **Backend (crs-backend/)**: An Express.js Node.js server with Sequelize ORM

### Current Status

The project is in active development with multiple features implemented including:
- User authentication and authorization
- Classroom management
- Resource management (12+ resource types)
- Video tracking and question answering
- Assessment management
- Student progress tracking
- Stripe payment integration
- Dashboard analytics
- Ticket management system

---

## Technology Stack

### Frontend Stack
```
Framework: Next.js 14.2.3 (React 18.3.1)
Language: TypeScript
State Management: Redux (@reduxjs/toolkit 2.2.1)
Authentication: NextAuth 4.24.6
Form Handling: React Hook Form 7.50.1
UI Components: Radix UI, Custom Component Library
Styling: Tailwind CSS 3.4.3 with PostCSS
Rich Text Editor: Jodit React 4.1.2
Charts: Recharts 2.12.7
Media Player: React Player 2.16.0
Utilities: Axios 1.6.7, Lodash, Mammoth (document parsing)
Document Export: HTML-to-DOCX 1.8.0
```

### Backend Stack
```
Runtime: Node.js (Latest LTS)
Framework: Express.js 4.18.2
Language: JavaScript
Database: PostgreSQL 11+
ORM: Sequelize 6.35.2
Authentication: JSON Web Tokens (jsonwebtoken 9.0.2)
Encryption: Bcrypt 5.1.1
Validation: Joi 17.12.1
Email Service: Nodemailer 6.9.8
Cron Jobs: Node-cron 3.0.3
Payment Processing: Stripe 16.1.0
Logging: Winston 3.13.0, Morgan 1.10.0
Process Manager: PM2 (via ecosystem.config.js)
Security: Cookie-parser, CORS, Helmet
```

---

## Architecture Overview

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    Client Layer                              │
│                  (Next.js Frontend)                          │
│  ┌─────────────────────────────────────────────────────────┐ │
│  │ Pages / Modules / Components / Redux Store             │ │
│  └────────────────────┬────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
                         │
                    Axios / Fetch
                         │
┌─────────────────────────────────────────────────────────────┐
│                    API Gateway Layer                          │
│                 (Next.js API Routes)                          │
└────────────────────┬────────────────────────────────────────┘
                     │
┌─────────────────────────────────────────────────────────────┐
│              Express.js Backend Server                        │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Routes → Controllers → Services → Models             │  │
│  └───────────────────┬───────────────────────────────────┘  │
│                      │                                        │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ Middlewares: Auth, RBAC, Validation, Logging         │  │
│  └───────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
                     │
        ┌────────────┼────────────┐
        │            │            │
    PostgreSQL   Stripe API    AWS S3
    (Primary DB) (Payments)   (File Storage)
```

### Project Structure

**Frontend (crs/)**
```
crs/
├── app/
│   ├── (auth)/              # Authentication pages
│   ├── (home)/              # Main application routes
│   ├── api/                 # API integration layer
│   │   ├── auth/
│   │   ├── classroom/
│   │   ├── dashboard/
│   │   ├── resource/
│   │   ├── student/
│   │   ├── school/
│   │   └── video/
│   ├── components/
│   │   ├── common/          # Reusable UI components
│   │   └── ui/              # Radix UI components
│   ├── modules/             # Feature modules
│   │   ├── auth/
│   │   ├── classroom/
│   │   ├── dashboard/
│   │   ├── learning/
│   │   ├── resources/
│   │   ├── standard/
│   │   └── users/
│   └── assets/              # Icons and images
├── lib/
│   ├── react-redux/         # Redux configuration
│   ├── next-auth/           # NextAuth setup
│   └── utils.ts             # Utility functions
├── tailwind.config.ts       # Styling configuration
└── tsconfig.json            # TypeScript configuration
```

**Backend (crs-backend/)**
```
crs-backend/
├── controllers/             # Request handlers (13 modules)
│   ├── auth-controller.js
│   ├── classroom-controller.js
│   ├── dashboard-controller.js
│   ├── question-controller.js
│   ├── resource-controller.js
│   ├── school-controller.js
│   ├── standard-controller.js
│   ├── student-controller.js
│   ├── user-controller.js
│   ├── video-controller.js
│   ├── videoQuestionAnswer-controller.js
│   ├── assessmentAnswer-controller.js
│   └── stripe.js
├── services/               # Business logic layer (13 modules)
│   └── helper/
├── models/                 # Sequelize models (21+ models)
├── routes/                 # Express route definitions (12 routes)
├── migrations/             # Database schema migrations (40+)
├── seeders/                # Database seed data
├── middlewares/
│   ├── rbac/               # Role-Based Access Control
│   └── validators/         # Request validation (Joi)
├── cronJobs/               # Scheduled tasks
├── utils/                  # Utility functions
├── Logs/                   # Logging configuration (Winston)
├── database/               # Database configuration
└── index.js                # Express app entry point
```

---

## Core Features & Modules

### 1. Authentication & Authorization Module

**Features:**
- User registration (signup) with role selection
- Email-based user invitations
- Secure password authentication with bcrypt hashing
- JWT-based token authentication
- NextAuth integration for session management
- OTP code generation and verification
- Invite token management with expiration

**Components:**
- `auth-controller.js` - Authentication logic
- `auth-service.js` - Authentication business logic
- `auth-routes.js` - Authentication endpoints
- `/app/(auth)/` - Frontend authentication pages

**Key Endpoints:**
```
POST   /auth/signup                    - User registration
POST   /auth/login                     - User login
POST   /auth/invite                    - Send user invitation
POST   /auth/signup/:token             - Signup with invitation
POST   /auth/verify-otp                - OTP verification
```

### 2. User Management Module

**Features:**
- User profile management
- User listing and filtering
- Role-based user creation
- User image/profile picture management
- User account updates
- Multiple role support (Student, Teacher, School, Admin)

**User Roles:**
```javascript
ROLES = {
    STUDENT: 'student',
    TEACHER: 'teacher',
    SCHOOL: 'school',
    ADMIN: 'admin'
}
```

**Database Model:**
```
User
├── id (UUID)
├── name
├── email (unique)
├── password (hashed)
├── role (enum: student, teacher, school, admin)
├── school_id (nullable, for school users)
├── image (profile picture URL)
└── timestamps (createdAt, updatedAt)
```

### 3. School Management Module

**Features:**
- School profile creation and management
- School-specific resource management
- Teacher management within schools
- Classroom oversight
- Course/Standard management
- Ticket/Support system
- Payment tracking and billing
- School analytics and reporting

**Key Endpoints:**
```
POST   /school/create                  - Create school
GET    /school/:id                     - Get school details
PUT    /school/update                  - Update school
GET    /school/list-teacher            - List teachers
GET    /school/get-courses             - Get school courses
POST   /school/create-ticket           - Create support ticket
GET    /school/list-ticket             - List tickets
```

### 4. Classroom Management Module

**Features:**
- Classroom creation and management
- Student enrollment in classrooms
- Classroom status management (active/inactive)
- Standard/Course assignment to classrooms
- Classroom-specific resource access
- Student progress tracking per classroom
- Bulk student enrollment

**Database Models:**
```
Classroom
├── id (UUID)
├── name
├── teacherId (FK)
├── schoolId (FK)
├── status (active/inactive)
└── timestamps

ClassroomStudent
├── id (UUID)
├── classroomId (FK)
├── studentId (FK)
└── timestamps

ClassroomCourses
├── id (UUID)
├── classroomId (FK)
├── standardId (FK)
└── timestamps
```

**Key Endpoints:**
```
POST   /classroom/create                    - Create classroom
GET    /classroom/:id                       - Get classroom details
GET    /classroom/teacher/:teacherid        - Get teacher's classrooms
POST   /classroom/add-student               - Add student to classroom
DELETE /classroom/remove-student            - Remove student
PUT    /classroom/assign-standard           - Assign course to classroom
```

### 5. Learning Standards Module

**Features:**
- Create and manage learning standards (courses)
- Topic organization within standards
- Daily upload scheduling
- Resource assignment to topics
- Standard progress tracking
- Teacher's learning plan creation
- Standard publishing and visibility controls

**Database Models:**
```
Standard
├── id (UUID)
├── name
├── description
├── createdBy (teacherId)
├── schoolId (FK)
└── timestamps

Topic
├── id (UUID)
├── standardId (FK)
├── name
├── description
└── timestamps

DailyUpload
├── id (UUID)
├── topicId (FK)
├── date
├── description
└── timestamps
```

### 6. Resource Management Module

**Features:**
- Multi-type resource support (12 resource types)
- Resource creation, update, and deletion
- Resource filtering and searching
- Topic-based resource organization
- Resource versioning and release control
- Resource metadata (duration, marks, deadline)
- AWS S3 integration for file storage
- Thumbnail/preview image support

**Supported Resource Types:**
```javascript
RESOURCE_TYPES = {
    SLIDESHOW: "slideshow",
    VIDEO: "video",
    WORKSHEET: "worksheet",
    QUIZ: "quiz",
    ASSIGNMENT: "assignment",
    LAB: "lab",
    STATION: "station",
    ACTIVITY: "activity",
    GUIDED_NOTE: "guided-note",
    FORMATIVE_ASSESSMENT: "formative-assessment",
    SUMMARIZE_ASSESSMENT: "summarize-assessment",
    DATA_TRACKER: "data-tracker"
}
```

**Database Model:**
```
Resource
├── id (UUID)
├── name
├── url
├── type (enum)
├── topic
├── thumbnailURL
├── duration
├── totalMarks
├── deadline
├── status (show/hide)
└── timestamps
```

**Key Endpoints:**
```
POST   /resource/create                 - Create resource
GET    /resource/list                   - Get resources (paginated)
GET    /resource/:id                    - Get resource details
PUT    /resource/update                 - Update resource
DELETE /resource/:id                    - Delete resource
GET    /resource/count                  - Get resource count by topic
GET    /resource/by-type                - Filter resources by type
```

### 7. Video Management Module

**Features:**
- Video resource creation and management
- Topic assignment to videos
- Video-specific questions attachment
- Video metadata (duration, thumbnail)
- Video tracking and progress monitoring
- Video player integration
- Question integration with videos

**Database Models:**
```
Video
├── id (UUID)
├── resourceId (FK)
├── thumbnailURL
└── timestamps

VideoQuestionAnswer
├── id (UUID)
├── userId (FK)
├── videoId (FK)
├── questionId (FK)
├── answer
├── weightage (marks obtained)
└── timestamps

VideoTracking
├── id (UUID)
├── studentId (FK)
├── videoId (FK)
├── standardId (FK)
├── lastSeenTime
├── watchedDuration
└── timestamps
```

**Key Endpoints:**
```
POST   /video/create                    - Create video
GET    /video/list                      - Get all videos
GET    /video/:id                       - Get video details
POST   /video/add-topics                - Add topics to video
POST   /video/answer                    - Submit video question answer
GET    /student/video                   - Get student's video progress
```

### 8. Questions & Assessment Module

**Features:**
- Question creation and management
- Question types and difficulty levels
- Question assignment to resources
- Assessment answer tracking
- Student response recording
- Grade calculation and weightage
- Formative and summative assessments

**Database Models:**
```
Question
├── id (UUID)
├── videoId (FK)
├── title
├── type (MCQ, essay, etc.)
├── content
├── difficulty
└── timestamps

AssessmentAnswer
├── id (UUID)
├── userId (FK)
├── questionId (FK)
├── answer
├── weightageObtained
└── timestamps
```

### 9. Student Dashboard & Progress Tracking

**Features:**
- Personalized dashboard for students
- Standard progress overview
- Resource completion status
- Assessment performance tracking
- Overall performance metrics
- Daily progress calculation
- Learning plan assignment display

**Dashboard Metrics:**
- Standards count
- Overall performance percentage
- Completed resources
- Active assessments
- Classroom information
- Learning progress visualization

**Database Model:**
```
DailyProgress
├── id (UUID)
├── studentId (FK)
├── date
├── progressPercentage
├── resourcesCompleted
├── assessmentsCompleted
└── timestamps
```

### 10. Teacher Dashboard & Management

**Features:**
- Classroom overview
- Student performance summary
- Resource management
- Standard creation and assignment
- Classroom analytics
- Student progress monitoring
- Attendance and engagement tracking

**Dashboard Summaries:**
- Total classrooms
- Total students
- Active learning plans
- Average student performance
- Resource distribution

### 11. Admin Dashboard

**Features:**
- System-wide statistics
- User management
- School management
- Resource oversight
- Payment/Billing tracking
- System health monitoring
- User activity logs

**Admin Summaries:**
- Total users count
- Total schools
- Total resources
- Total classrooms
- Platform-wide analytics

### 12. Payment & Billing Integration

**Features:**
- Stripe payment processing
- Checkout session creation
- Webhook handling for payment confirmation
- Payment status tracking
- Order management
- Classroom activation through payments

**Implementation:**
- `stripe.js` controller - Payment handling
- Stripe API integration for checkout
- Webhook endpoint for payment confirmation
- Payment status persistence to database

### 13. Ticket/Support System

**Features:**
- School support ticket creation
- Ticket status tracking
- Ticket assignment and resolution
- Communication logging
- Issue categorization

**Database Model:**
```
Ticket
├── id (UUID)
├── submitted_by (FK)
├── schoolId (FK)
├── title
├── description
├── status
└── timestamps
```

---

## Database Schema

### Core Models (21+ Models)

**User Management:**
- User
- OtpCode
- InviteToken
- Invite

**School & Organization:**
- School
- Classroom
- ClassroomStudent
- ClassroomCourses

**Learning Content:**
- Standard
- Topic
- TopicDailyUpload
- DailyUpload
- Resource
- Video

**Learning Tracking:**
- VideoTracking
- VideoQuestionAnswer
- AssessmentAnswer
- DailyProgress

**Assessment:**
- Question
- AssessmentResourcesDetail

**Support & Billing:**
- Ticket
- Payment (implied)

**Relationships:**
- User → School (many-to-one)
- User → Classroom (teacher-many)
- Classroom → ClassroomStudent (one-many)
- Standard → Topic (one-many)
- Topic → Resource (one-many)
- Video → VideoQuestionAnswer (one-many)
- User → VideoQuestionAnswer (one-many)

### Database Configuration

**Primary Database:** PostgreSQL 11+
**Port:** 5432 (default)
**ORM:** Sequelize 6.35.2
**Connection Pooling:** Enabled
**Migrations:** 40+ schema migrations
**Seeds:** Admin user and test data

---

## API Endpoints & Routes

### Authentication Routes (/auth)
```
POST   /auth/signup                    Sign up new user
POST   /auth/login                     User login
POST   /auth/invite                    Send invitation
POST   /auth/signup/:token             Complete signup with token
POST   /auth/verify-otp                Verify OTP code
```

### User Routes (/user)
```
GET    /user/profile                   Get user profile
PUT    /user/update                    Update user profile
GET    /user/list                      List users
GET    /user/:id                       Get user by ID
```

### School Routes (/school)
```
POST   /school/create                  Create school
GET    /school/:id                     Get school details
PUT    /school/update                  Update school
GET    /school/list-teacher            List school teachers
GET    /school/get-courses             Get school courses
POST   /school/create-ticket           Create support ticket
PUT    /school/update-ticket           Update ticket
GET    /school/get-ticket              Get ticket details
GET    /school/list-ticket             List all tickets
```

### Resource Routes (/resource)
```
POST   /resource/create                Create resource
GET    /resource/list                  Get resources (paginated)
GET    /resource/:id                   Get resource by ID
PUT    /resource/update                Update resource
DELETE /resource/:id                   Delete resource
GET    /resource/count                 Get resource count
GET    /resource/by-type               Filter by type
GET    /resource/by-name               Search by name
```

### Video Routes (/video)
```
POST   /video/create                   Create video
GET    /video/list                     Get all videos
GET    /video/:id                      Get video details
POST   /video/add-topics               Add topics to video
GET    /video/by-topic                 Get videos by topic
```

### Question Routes (/question)
```
POST   /question/create                Create question
GET    /question/list                  Get questions
GET    /question/:id                   Get question by ID
PUT    /question/update                Update question
DELETE /question/:id                   Delete question
```

### Standard Routes (/standard)
```
POST   /standard/create                Create standard
GET    /standard/list                  Get standards
GET    /standard/:id                   Get standard by ID
PUT    /standard/update                Update standard
DELETE /standard/:id                   Delete standard
```

### Classroom Routes (/classroom)
```
POST   /classroom/create               Create classroom
GET    /classroom/:id                  Get classroom details
GET    /classroom/teacher/:id          Get teacher's classrooms
POST   /classroom/add-student          Add student to classroom
DELETE /classroom/remove-student       Remove student
PUT    /classroom/assign-standard      Assign standard to classroom
GET    /classroom/students             Get classroom students
```

### Student Routes (/student)
```
GET    /student/standards              Get student's standards
GET    /student/video                  Get student's video progress
POST   /student/save-video             Save video progress
GET    /student/standard/:id           Get standard progress
GET    /student/resources              Get assigned resources
```

### Dashboard Routes (/dashboard)
```
GET    /dashboard/teacher              Get teacher dashboard data
GET    /dashboard/admin                Get admin dashboard data
GET    /dashboard/student              Get student dashboard data
```

### Assessment Routes (/assessmentAnswer)
```
POST   /assessment-answer/create       Submit assessment answer
GET    /assessment-answer/list         Get answers
```

### Video Question Answer Routes (/videoQuestionAnswer)
```
POST   /video-question-answer/create   Submit answer
GET    /video-question-answer/list     Get answers
```

---

## User Roles & Access Control

### Role Hierarchy

```
┌─────────────────────────────────────────────────┐
│                    ADMIN                        │
│  • Full system access                          │
│  • User management                             │
│  • School oversight                            │
│  • System configuration                        │
└──────────────────┬──────────────────────────────┘
                   │
    ┌──────────────┴──────────────┐
    │                             │
┌───▼─────────────────┐   ┌──────▼──────────────┐
│      SCHOOL         │   │      TEACHER       │
│  • Manage teachers  │   │  • Create/manage   │
│  • View analytics   │   │    classrooms      │
│  • Manage payments  │   │  • Assign resources│
│  • Support tickets  │   │  • Track students  │
└───┬─────────────────┘   └──────┬──────────────┘
    │                             │
    │         ┌───────────────────┘
    │         │
    └────┬────┴────┐
         │         │
    ┌────▼──┐   ┌──▼────┐
    │STUDENT│   │ No    │
    │ (Temp)│   │ Access│
    └───────┘   └───────┘
```

### RBAC Implementation

**Middleware Stack:**
```
roleBasedAccess.setUser        → Extracts user from JWT
roleBasedAccess.VerifyAllowedRole → Checks role permissions
```

**Example Route Protection:**
```javascript
router.get('/list-teacher',
    roleBasedAccess.setUser,
    roleBasedAccess.VerifyAllowedRole([ROLES.ADMIN, ROLES.SCHOOL]),
    schoolController.listTeacher
);
```

**Access Control by Module:**

| Module | Admin | School | Teacher | Student |
|--------|-------|--------|---------|---------|
| Users | R/W | R | - | R |
| Schools | R/W | R/W | - | - |
| Classroom | R | R/W | R/W | R |
| Standards | R | R | R/W | R |
| Resources | R/W | R | R/W | R |
| Videos | R/W | R | R/W | R |
| Dashboard | R | R | R | R |
| Assessments | R | R | R/W | R/W |
| Tickets | R | R/W | - | - |
| Payments | R | R | - | - |

---

## Frontend Implementation

### Technology & Architecture

**Framework:** Next.js 14 with App Router
**Language:** TypeScript
**State Management:** Redux with Redux Toolkit
**Authentication:** NextAuth.js 4.x
**Styling:** Tailwind CSS 3 with custom components

### Main Modules

**1. Authentication Module (`/app/(auth)/)`**
- Login page
- Signup flow (student, teacher, school)
- Multi-step school signup
- OTP verification
- Password reset

**2. Home Module (`/app/(home)/)`**
- Main application routes
- Protected pages
- Redirects based on role

**3. Dashboard Module**
- **Teacher Dashboard** - Classroom overview, student analytics
- **Student Dashboard** - Standards, progress, assignments
- **Admin Dashboard** - System statistics, user management
- **School Dashboard** - Analytics, teacher management, payments

**4. Learning Module (`modules/learning/`)**
- Learning interface
- Video player
- Question navigation
- Progress tracking
- Checkpoint system

**5. Resources Module (`modules/resources/`)**
- Resource listing and filtering
- Resource type filtering
- Download functionality
- Resource cards and tables
- Upload modal

**6. Standard Module (`modules/standard/`)**
- Standard creation/management
- Topic management
- Daily upload scheduling
- Standard progression view
- Teacher vs. Admin view

**7. Classroom Module**
- Classroom creation
- Student enrollment
- Class settings
- Student list view
- Standard assignment

**8. Teacher Standards Module (`modules/teacher-standards/`)**
- Topics list
- Resources per topic
- Add resource modal
- Resource card display
- Resource management

**9. Profile & Settings Module (`modules/profile/`, `modules/setting/`)**
- User profile display
- Settings page
- Account management

**10. Users Module (`modules/users/`)**
- User listing
- Add user modal
- User management
- Role assignment

### Component Library

**Common Components** (`components/common/`)
- AppInput - Text input wrapper
- AppDropDown - Select component
- Button - Custom button
- Card - Card wrapper
- Searchbar - Search interface
- Table - Data table
- Modal - Dialog component
- Pagination - Page navigation
- Filter - Filter controls
- Loader - Loading states
- ButtonLoader - Loading button
- ModalHeader - Modal title bar

**UI Components** (`components/ui/`)
- Radix UI based components
- Checkbox
- Label
- Slot

### Redux Store Structure

```typescript
interface ReduxState {
    auth: {
        user?: User;
        loading: boolean;
        error?: string;
    };
    [feature]: {
        data?: object;
        loading: boolean;
        error?: string;
    };
}
```

**Key Actions:**
- User login/signup
- Fetch user profile
- Classroom operations
- Resource operations
- Dashboard data fetch

### Next.js API Integration Layer

**Structure:** `/app/api/[feature]/index.ts`

**Features:**
- Axios-based HTTP client
- Base URL configuration
- Authorization header management
- Error handling
- Response/Request transformation

**API Modules:**
```
api/
├── auth/          - Authentication endpoints
├── classroom/     - Classroom operations
├── dashboard/     - Dashboard data
├── resource/      - Resource operations
├── school/        - School operations
├── student/       - Student data
├── video/         - Video operations
└── user/          - User operations
```

### Styling & UI Design

**Tailwind Configuration:**
- Custom color palette
- Responsive breakpoints
- Component variants
- Animation utilities

**Color Scheme:**
- Primary: Blue tones
- Secondary: Gray scale
- Success: Green
- Warning: Yellow/Orange
- Error: Red
- Background: Light gray
- Text: Dark gray/black

**Responsive Design:**
- Mobile-first approach
- Breakpoints: mobile, tablet, desktop
- Flexbox and Grid layouts
- Tailwind responsive utilities

---

## Key Technical Implementations

### 1. Authentication Flow

**JWT Implementation:**
```javascript
// Token Generation
const generateAccessToken = (payload) => {
    return jwt.sign(payload, process.env.JWT_SECRET, {
        expiresIn: '24h'
    });
};

// Token Verification
const verifyToken = (token) => {
    return jwt.verify(token, process.env.JWT_SECRET);
};
```

**NextAuth Configuration:**
- Session-based authentication
- JWT provider integration
- Custom callbacks for authorization
- Session refresh logic

### 2. Data Validation

**Joi Validators:**
```javascript
// Example: Resource Creation Validator
const createResource = celebrate({
    [Segments.BODY]: Joi.object().keys({
        name: Joi.string().required(),
        url: Joi.string().required(),
        type: Joi.string().valid(...RESOURCE_TYPES).required(),
        topic: Joi.string().required(),
        thumbnailURL: Joi.string(),
        duration: Joi.string(),
        totalMarks: Joi.number(),
        deadline: Joi.number(),
        accesstoken: Joi.string().required()
    }).unknown()
});
```

**Validation Middleware:**
- Applied at route level
- Segmented validation (body, headers, query)
- Custom error messages
- Type coercion support

### 3. Error Handling

**Response Handlers:**
```javascript
handleSuccessResponse(res, statusCode, data)
handleErrorResponse(res, statusCode, message)
handleInternalServerError(res)
```

**Error Types:**
- 400: Bad Request (validation errors)
- 401: Unauthorized (auth required)
- 403: Forbidden (insufficient permissions)
- 404: Not Found (resource not found)
- 409: Conflict (duplicate/constraint violation)
- 500: Internal Server Error

### 4. Logging System

**Winston Logger Configuration:**
```javascript
const logger = winston.createLogger({
    level: process.env.LOG_LEVEL || 'info',
    format: winston.format.json(),
    transports: [
        new winston.transports.File({ 
            filename: 'logs/error.log', 
            level: 'error' 
        }),
        new winston.transports.File({ 
            filename: 'logs/combined.log' 
        })
    ]
});
```

**Morgan Middleware:**
- HTTP request logging
- Response time tracking
- Status code monitoring

### 5. Database Transaction Management

**Transaction Usage:**
```javascript
const transaction = await db.sequelize.transaction();
try {
    // Multiple operations
    await Model.update(data, { transaction });
    await Model2.create(data, { transaction });
    await transaction.commit();
} catch (error) {
    await transaction.rollback();
}
```

### 6. AWS S3 Integration

**File Storage:**
- Profile pictures
- Resource files
- Video thumbnails
- Default image storage

**Configuration:**
```
Bucket: crs-data-storage-bucket
Region: ap-southeast-2
Base URL: https://crs-data-storage-bucket.s3.ap-southeast-2.amazonaws.com/
```

### 7. Cron Jobs

**Scheduled Tasks:**
```javascript
// dailyProgress-Job.js
node-cron.schedule('0 0 * * *', () => {
    // Calculate daily progress for all students
});
```

### 8. Payment Processing

**Stripe Integration:**
```javascript
const session = await stripe.checkout.sessions.create({
    payment_method_types: ['card'],
    mode: 'payment',
    line_items: [...],
    success_url: 'https://...',
    cancel_url: 'https://...'
});
```

**Webhook Handling:**
- Signature verification
- Event type processing
- Idempotent operations
- Status persistence

### 9. Middleware Stack

**Request Processing Pipeline:**

```
Incoming Request
    ↓
CORS Middleware
    ↓
Body Parser (JSON/URL-encoded)
    ↓
Cookie Parser
    ↓
Morgan Logger
    ↓
Route Specific:
  - setUser (Extract JWT)
  - VerifyAllowedRole (RBAC)
  - Joi Validation
    ↓
Controller Handler
    ↓
Response Handler
```

---

## Deployment & Configuration

### Environment Variables

**Backend (.env):**
```
NODE_ENV=production
PORT=5000
DATABASE_URL=postgresql://...
JWT_SECRET=your-secret-key
STRIPE_PRIVATE_KEY=sk_live_...
STRIPE_WEBHOOK_SECRET=whsec_...
AWS_ACCESS_KEY_ID=...
AWS_SECRET_ACCESS_KEY=...
AWS_REGION=ap-southeast-2
MAIL_USER=noreply@...
MAIL_PASSWORD=...
LOG_LEVEL=info
```

**Frontend (.env.local):**
```
NEXT_PUBLIC_BASE_URL=https://api.crsci.org
NEXTAUTH_URL=https://app.crsci.org
NEXTAUTH_SECRET=your-secret
```

### CORS Configuration

```javascript
app.use(cors({
    origin: [
        'http://localhost:3000',
        'https://app.crsci.org'
    ],
    credentials: true
}));
```

### Database Migrations

**Migration Command:**
```bash
npx sequelize-cli db:migrate
```

**Seeding:**
```bash
npx sequelize-cli db:seed:all
```

### Process Management

**PM2 Configuration** (`ecosystem.config.js`):
```javascript
module.exports = {
    apps: [{
        name: 'crs-backend',
        script: './index.js',
        instances: 'max',
        exec_mode: 'cluster',
        env: {
            NODE_ENV: 'production'
        }
    }]
};
```

**Deployment:**
```bash
pm2 start ecosystem.config.js
pm2 logs
pm2 monit
```

### Build & Deployment

**Frontend Build:**
```bash
npm run build
npm start
```

**Backend Deployment:**
```bash
npm install
npm start  # or pm2 start ecosystem.config.js
```

### Production Considerations

1. **Security:**
   - HTTPS/TLS encryption
   - Environment variable protection
   - SQL injection prevention (Sequelize)
   - XSS protection (React sanitization)
   - CSRF tokens for state-changing operations

2. **Performance:**
   - Database indexing on frequently queried fields
   - Redis caching (future enhancement)
   - CDN for static assets
   - API rate limiting
   - Connection pooling

3. **Monitoring:**
   - Error tracking (recommended: Sentry)
   - Performance monitoring
   - Uptime monitoring
   - Log aggregation

4. **Scalability:**
   - Horizontal scaling with PM2 cluster mode
   - Load balancing
   - Database read replicas
   - Microservices ready architecture

---

## Conclusion

### Project Strengths

1. **Comprehensive Feature Set:** 13+ major modules covering all aspects of curriculum management
2. **Enterprise Architecture:** Well-structured with clear separation of concerns
3. **Security:** Role-based access control, encrypted passwords, JWT authentication
4. **Scalability:** Designed for growth with modern frameworks and patterns
5. **Integration:** Stripe payments, AWS S3 storage, email notifications
6. **Development Experience:** TypeScript, Redux, Next.js provide excellent DX
7. **Database Design:** Normalized schema with proper relationships and migrations

### Areas of Excellence

- **User Management:** Flexible role system supporting multiple user types
- **Resource Diversity:** 12+ resource types for varied learning materials
- **Progress Tracking:** Comprehensive student progress and engagement metrics
- **Payment Integration:** Professional payment processing with Stripe
- **Learning Organization:** Well-structured standards, topics, and daily uploads
- **API Design:** RESTful endpoints with consistent response formats
- **Code Organization:** Modular structure with services, controllers, and middleware

### Recommended Future Enhancements

1. **Caching Layer:** Implement Redis for frequently accessed data
2. **Real-time Features:** WebSocket integration for live notifications
3. **AI/ML:** Student recommendation engine for personalized learning
4. **Mobile App:** React Native mobile applications
5. **Analytics Dashboard:** Advanced reporting and data visualization
6. **Testing:** Comprehensive unit and integration test coverage
7. **Documentation:** API documentation with Swagger/OpenAPI
8. **Internationalization:** Multi-language support
9. **Video Streaming:** Adaptive bitrate streaming for better video delivery
10. **Advanced Search:** Full-text search capabilities

### Summary

CRS is a mature, well-architected Learning Management System ready for production deployment. The combination of modern technologies, comprehensive features, and sound architectural decisions positions the project well for educational institutions of all sizes. The modular design ensures maintainability and extensibility as requirements evolve.

---

**Report Generated:** December 15, 2025  
**Repository:** https://github.com/abrauf18/crs-backend  
**Frontend Source:** crs/  
**Backend Source:** crs-backend/

---

## Appendix: Quick Reference

### Installation & Setup

```bash
# Backend Setup
cd crs-backend
npm install
npx sequelize-cli db:migrate
npm start

# Frontend Setup
cd crs
npm install
npm run dev
```

### Key Files Reference

| File | Purpose |
|------|---------|
| `index.js` | Express app initialization |
| `models/index.js` | Sequelize model loader |
| `Logs/logger.js` | Winston logging setup |
| `middlewares/rbac/` | RBAC middleware |
| `utils/enumTypes.js` | Constant definitions |
| `package.json` | Dependencies (13 major, 25 total) |

### Important Contacts & Resources

- **Database:** PostgreSQL 11+
- **Payment:** Stripe API
- **Storage:** AWS S3 (ap-southeast-2)
- **Email:** Nodemailer (SMTP)

---

*End of Report*
