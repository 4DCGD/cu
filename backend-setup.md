# Backend Setup for CuraFinder

## Overview
This document provides instructions for setting up a backend server to connect your React frontend to the PostgreSQL database.

## Prerequisites
- ✅ PostgreSQL database set up (completed)
- ✅ Node.js installed
- ✅ npm or yarn package manager

## Option 1: Express.js Backend (Recommended)

### 1. Create Backend Directory
```bash
mkdir curafinder-backend
cd curafinder-backend
npm init -y
```

### 2. Install Dependencies
```bash
npm install express cors dotenv pg bcryptjs jsonwebtoken helmet morgan
npm install --save-dev nodemon @types/node @types/express
```

### 3. Create Basic Server Structure
```
curafinder-backend/
├── src/
│   ├── config/
│   │   └── database.js
│   ├── routes/
│   │   ├── clinics.js
│   │   ├── reviews.js
│   │   └── users.js
│   ├── controllers/
│   │   ├── clinicController.js
│   │   ├── reviewController.js
│   │   └── userController.js
│   ├── middleware/
│   │   ├── auth.js
│   │   └── validation.js
│   └── app.js
├── .env
└── package.json
```

### 4. Environment Configuration (.env)
```env
# Server Configuration
PORT=3001
NODE_ENV=development

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=curafinder
DB_USER=curafinder_user
DB_PASSWORD=curafinder_password

# JWT Configuration
JWT_SECRET=your-super-secret-jwt-key-here
JWT_EXPIRES_IN=7d

# CORS Configuration
CORS_ORIGIN=http://localhost:3000
```

### 5. Database Connection (src/config/database.js)
```javascript
const { Pool } = require('pg');
require('dotenv').config();

const pool = new Pool({
  host: process.env.DB_HOST,
  port: process.env.DB_PORT,
  database: process.env.DB_NAME,
  user: process.env.DB_USER,
  password: process.env.DB_PASSWORD,
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000,
});

pool.on('connect', () => {
  console.log('Connected to PostgreSQL database');
});

pool.on('error', (err) => {
  console.error('Unexpected error on idle client', err);
  process.exit(-1);
});

module.exports = pool;
```

### 6. Main Server File (src/app.js)
```javascript
const express = require('express');
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 3001;

// Middleware
app.use(helmet());
app.use(cors({
  origin: process.env.CORS_ORIGIN || 'http://localhost:3000',
  credentials: true
}));
app.use(morgan('combined'));
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.use('/api/clinics', require('./routes/clinics'));
app.use('/api/reviews', require('./routes/reviews'));
app.use('/api/users', require('./routes/users'));

// Health check
app.get('/api/health', (req, res) => {
  res.json({ status: 'OK', message: 'CuraFinder API is running' });
});

// Error handling middleware
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ 
    error: 'Something went wrong!',
    message: process.env.NODE_ENV === 'development' ? err.message : 'Internal server error'
  });
});

app.listen(PORT, () => {
  console.log(`🚀 CuraFinder backend server running on port ${PORT}`);
  console.log(`📊 Database: ${process.env.DB_NAME} on ${process.env.DB_HOST}:${process.env.DB_PORT}`);
});
```

### 7. Add Scripts to package.json
```json
{
  "scripts": {
    "start": "node src/app.js",
    "dev": "nodemon src/app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

## Option 2: Quick Start with Existing Tools

### Using pgAdmin (GUI)
1. Open pgAdmin
2. Connect to your PostgreSQL server
3. Navigate to the `curafinder` database
4. Use the Query Tool to run SQL commands
5. View and edit data through the interface

### Using Command Line
```bash
# Connect to database
& "C:\Program Files\PostgreSQL\17\bin\psql.exe" -U postgres -d curafinder

# View tables
\dt

# View table structure
\d clinics

# Run queries
SELECT * FROM clinics;
```

## Testing the Connection

### 1. Start Backend Server
```bash
cd curafinder-backend
npm run dev
```

### 2. Test API Endpoints
```bash
# Health check
curl http://localhost:3001/api/health

# Get clinics
curl http://localhost:3001/api/clinics

# Get reviews
curl http://localhost:3001/api/reviews
```

### 3. Update Frontend Configuration
In your React app, update the `.env.local` file:
```env
REACT_APP_API_URL=http://localhost:3001/api
```

## Next Steps

1. **Implement API Routes**: Create the actual endpoints for clinics, reviews, and users
2. **Add Authentication**: Implement JWT-based authentication for admin access
3. **Data Validation**: Add input validation and sanitization
4. **Error Handling**: Implement comprehensive error handling
5. **Testing**: Add unit and integration tests
6. **Deployment**: Prepare for production deployment

## Troubleshooting

### Common Issues
- **Connection refused**: Check if PostgreSQL service is running
- **Authentication failed**: Verify database credentials
- **Port already in use**: Change the backend port in .env
- **CORS errors**: Verify CORS_ORIGIN configuration

### Useful Commands
```bash
# Check PostgreSQL service status (Windows)
sc query postgresql-x64-17

# Start PostgreSQL service (Windows)
net start postgresql-x64-17

# Check if port is in use
netstat -an | findstr :3001
```

## Security Considerations

1. **Environment Variables**: Never commit .env files to version control
2. **Database Passwords**: Use strong, unique passwords
3. **JWT Secrets**: Generate cryptographically secure JWT secrets
4. **CORS**: Restrict CORS origins to your frontend domain
5. **Input Validation**: Validate and sanitize all user inputs
6. **SQL Injection**: Use parameterized queries (pg library handles this)

## Performance Tips

1. **Connection Pooling**: Use connection pooling (already configured)
2. **Indexes**: Database indexes are already created
3. **Query Optimization**: Monitor slow queries and optimize
4. **Caching**: Consider adding Redis for caching
5. **Compression**: Enable gzip compression for responses
