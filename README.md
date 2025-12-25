# CRS - Curriculum Resource System

A comprehensive full-stack Learning Management System (LMS) designed to streamline curriculum delivery and resource management across schools and educational institutions.

## 🎯 Project Overview

CRS is an enterprise-grade educational platform that enables:

- **Schools**: Create and manage learning standards, curriculum, and billing
- **Teachers**: Organize classrooms, assign resources, and track student progress
- **Students**: Access personalized learning experiences and educational content
- **Administrators**: Oversee system operations and user management

## 🏗️ Architecture

The project is organized into two main components:

```
crsci/
├── crs/           # Next.js Frontend Application
└── crs-backend/   # Express.js Backend API
```

## 🛠️ Technology Stack

### Frontend (`crs/`)
- **Framework**: Next.js 13+ (React)
- **Styling**: Tailwind CSS
- **State Management**: Redux Toolkit
- **Form Handling**: React Hook Form
- **UI Components**: Radix UI
- **HTTP Client**: Axios
- **Authentication**: NextAuth.js
- **Rich Text Editor**: Jodit React
- **Document Export**: html-to-docx

### Backend (`crs-backend/`)
- **Runtime**: Node.js
- **Framework**: Express.js
- **ORM**: Sequelize
- **Database**: PostgreSQL
- **Authentication**: JWT (jsonwebtoken)
- **Password Hashing**: Bcrypt
- **Email Service**: Nodemailer
- **Job Scheduling**: node-cron
- **Validation**: Joi
- **CORS**: Enabled for cross-origin requests

### Infrastructure
- **Database**: PostgreSQL
- **File Storage**: AWS S3
- **Process Manager**: PM2 (via ecosystem.config.js)

## 📁 Project Structure

### Frontend Structure (`crs/`)
```
crs/
├── app/
│   ├── (auth)/          # Authentication pages
│   ├── (home)/          # Main application pages
│   ├── api/             # API routes
│   ├── components/      # React components
│   ├── assets/          # Static assets
│   └── modules/         # Feature modules
├── lib/
│   ├── custom-hooks/    # Custom React hooks
│   ├── next-auth/       # NextAuth configuration
│   ├── react-redux/     # Redux setup
│   └── utils.ts         # Utility functions
├── next.config.js       # Next.js configuration
├── tailwind.config.ts   # Tailwind CSS configuration
└── tsconfig.json        # TypeScript configuration
```

### Backend Structure (`crs-backend/`)
```
crs-backend/
├── controllers/         # Request handlers for different modules
├── models/              # Sequelize database models
├── routes/              # API route definitions
├── services/            # Business logic and database operations
├── middlewares/         # Express middlewares (RBAC, validation)
├── migrations/          # Database migrations
├── seeders/             # Database seeders
├── cronJobs/            # Scheduled jobs
├── Logs/                # Logging utilities
├── database/            # Database configuration
└── index.js             # Main application entry point
```

## 🔐 Key Features

### Authentication & Authorization
- User authentication via JWT tokens
- Role-Based Access Control (RBAC)
- Support for multiple user roles: Student, Teacher, School Admin, Super Admin
- Secure password hashing with Bcrypt

### Core Modules

1. **User Management**
   - User registration, login, and profile management
   - Role assignment and management

2. **School Management**
   - School creation and configuration
   - User invitations to schools
   - Billing and payment processing (Stripe integration)

3. **Curriculum Management**
   - Learning standards definition
   - Curriculum organization and structure
   - Resource categorization

4. **Classroom Management**
   - Class creation and student enrollment
   - Teacher assignment
   - Class progress tracking

5. **Content Management**
   - Video uploads and management
   - Document/resource uploads
   - Assessment questions
   - Video tracking and engagement metrics

6. **Assessment & Tracking**
   - Assessment creation and assignment
   - Student answer tracking
   - Daily progress monitoring
   - Performance analytics

7. **Dashboard**
   - Student dashboard with personalized content
   - Teacher dashboard with class analytics
   - Admin dashboard with system overview

## 🚀 Getting Started

### Prerequisites
- Node.js 16+ and npm/yarn
- PostgreSQL database
- AWS S3 bucket (for file storage)
- Stripe account (for payment processing)

### Backend Setup

1. Navigate to the backend directory:
```bash
cd crs-backend
```

2. Install dependencies:
```bash
npm install
```

3. Configure environment variables:
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. Run database migrations:
```bash
npm run migrate
```

5. Start the development server:
```bash
npm run dev
```

The backend API will be available at `http://localhost:5000` (or your configured port).

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd crs
```

2. Install dependencies:
```bash
npm install
```

3. Configure environment variables:
```bash
cp .env.example .env.local
# Edit .env.local with your backend API URL and NextAuth config
```

4. Start the development server:
```bash
npm run dev
```

The frontend will be available at `http://localhost:3000`.

## 📦 Available Scripts

### Backend
- `npm run dev` - Start development server with nodemon
- `npm run start` - Start production server
- `npm test` - Run tests

### Frontend
- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run start` - Start production server
- `npm run lint` - Run ESLint

## 🗄️ Database

The application uses PostgreSQL with Sequelize ORM. Key models include:

- **User** - User accounts and authentication
- **School** - Educational institutions
- **Classroom** - Classes within schools
- **Video** - Educational video content
- **Question** - Assessment questions
- **Resource** - Educational materials
- **Standard** - Learning standards
- **AssessmentAnswer** - Student answers to assessments
- **DailyProgress** - Daily progress tracking
- **Ticket** - Support tickets

Run migrations to set up the database schema:
```bash
npm run migrate
```

## 🔗 API Documentation

The backend provides RESTful API endpoints organized by feature:

- `/api/auth` - Authentication endpoints
- `/api/users` - User management
- `/api/schools` - School management
- `/api/classrooms` - Classroom operations
- `/api/videos` - Video management
- `/api/questions` - Question management
- `/api/resources` - Resource management
- `/api/assessments` - Assessment operations
- `/api/dashboard` - Dashboard data

## 🔐 Environment Variables

### Backend
```
PORT=5000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=crs_database
DB_USER=postgres
DB_PASSWORD=your_password
JWT_SECRET=your_jwt_secret
AWS_ACCESS_KEY_ID=your_aws_key
AWS_SECRET_ACCESS_KEY=your_aws_secret
STRIPE_SECRET_KEY=your_stripe_key
```

### Frontend
```
NEXT_PUBLIC_API_URL=http://localhost:5000
NEXTAUTH_SECRET=your_nextauth_secret
NEXTAUTH_URL=http://localhost:3000
```

## 🚢 Deployment

### Production Build

**Frontend:**
```bash
cd crs
npm run build
npm run start
```

**Backend:**
```bash
cd crs-backend
npm install --production
npm start
```

The project includes PM2 configuration (`ecosystem.config.js`) for process management in production.

## 📊 Project Status

This is an active development project with comprehensive architecture supporting enterprise-level educational platform requirements.

## 📝 Documentation

For detailed architecture and features analysis, see [PROJECT_REPORT.md](./PROJECT_REPORT.md).

## 📄 License

This project is licensed under the ISC License.

## 👥 Contributing

For contributions, please follow the project's code standards and create feature branches from the main branch.

## 📞 Support

For issues and questions, please refer to the project documentation or contact the project owner.

---

**Last Updated:** December 25, 2025
