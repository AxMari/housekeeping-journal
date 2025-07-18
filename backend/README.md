# Backend API

This directory contains the backend API for the Housekeeping Journal application.

## Planned Features

- **User Authentication**: JWT-based authentication system
- **Task Management**: CRUD operations for tasks and schedules
- **Calendar Integration**: API endpoints for calendar data
- **Professional Services**: Integration with housekeeping service providers
- **Database**: PostgreSQL with Prisma ORM
- **Real-time Updates**: WebSocket support for live updates

## Tech Stack (Planned)

- **Runtime**: Node.js
- **Framework**: Express.js or Fastify
- **Database**: PostgreSQL
- **ORM**: Prisma
- **Authentication**: JWT
- **Validation**: Zod
- **Testing**: Jest
- **Documentation**: OpenAPI/Swagger

## Development Status

🚧 **Under Development** 🚧

The backend API is currently in planning phase. This will be developed after the frontend is more complete.

## Structure (Planned)

```
backend/
├── src/
│   ├── controllers/     # Route controllers
│   ├── middleware/      # Custom middleware
│   ├── models/          # Database models
│   ├── routes/          # API routes
│   ├── services/        # Business logic
│   ├── utils/           # Utility functions
│   └── app.js           # Express app setup
├── prisma/              # Database schema and migrations
├── tests/               # Test files
├── package.json
└── README.md
```

## Getting Started

1. Install dependencies: `npm install`
2. Set up environment variables
3. Run database migrations: `npx prisma migrate dev`
4. Start development server: `npm run dev`

## API Endpoints (Planned)

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout

### Tasks
- `GET /api/tasks` - Get all tasks
- `POST /api/tasks` - Create new task
- `PUT /api/tasks/:id` - Update task
- `DELETE /api/tasks/:id` - Delete task

### Calendar
- `GET /api/calendar/events` - Get calendar events
- `POST /api/calendar/events` - Create calendar event
- `PUT /api/calendar/events/:id` - Update calendar event
- `DELETE /api/calendar/events/:id` - Delete calendar event

### Services
- `GET /api/services` - Get available services
- `POST /api/services/book` - Book a service
- `GET /api/services/bookings` - Get user bookings 