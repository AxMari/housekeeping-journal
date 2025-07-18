# API Documentation

This document describes the REST API endpoints for the Housekeeping Journal application.

## Base URL

- **Development**: `http://localhost:3001`
- **Production**: `https://api.housekeeping-journal.com`

## Authentication

The API uses JWT (JSON Web Tokens) for authentication. Include the token in the Authorization header:

```
Authorization: Bearer <your-jwt-token>
```

## Response Format

All API responses follow this format:

```json
{
  "success": true,
  "data": {
    // Response data
  },
  "message": "Optional message",
  "timestamp": "2024-01-01T00:00:00.000Z"
}
```

Error responses:

```json
{
  "success": false,
  "error": {
    "code": "ERROR_CODE",
    "message": "Human readable error message",
    "details": {}
  },
  "timestamp": "2024-01-01T00:00:00.000Z"
}
```

## HTTP Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `500` - Internal Server Error

## Endpoints

### Authentication

#### POST /auth/register
Register a new user.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword",
  "name": "John Doe"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "user-id",
      "email": "user@example.com",
      "name": "John Doe",
      "createdAt": "2024-01-01T00:00:00.000Z"
    },
    "token": "jwt-token"
  }
}
```

#### POST /auth/login
Login with existing credentials.

**Request Body:**
```json
{
  "email": "user@example.com",
  "password": "securepassword"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "user": {
      "id": "user-id",
      "email": "user@example.com",
      "name": "John Doe"
    },
    "token": "jwt-token"
  }
}
```

#### POST /auth/logout
Logout and invalidate token.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Response:**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

### Tasks

#### GET /tasks
Get all tasks for the authenticated user.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Query Parameters:**
- `page` (number) - Page number (default: 1)
- `limit` (number) - Items per page (default: 10)
- `status` (string) - Filter by status (completed, pending, all)
- `category` (string) - Filter by category
- `sort` (string) - Sort by field (createdAt, dueDate, priority)

**Response:**
```json
{
  "success": true,
  "data": {
    "tasks": [
      {
        "id": "task-id",
        "title": "Clean kitchen",
        "description": "Wipe counters and sweep floor",
        "status": "pending",
        "priority": "medium",
        "category": "cleaning",
        "dueDate": "2024-01-15T00:00:00.000Z",
        "completedAt": null,
        "createdAt": "2024-01-01T00:00:00.000Z",
        "updatedAt": "2024-01-01T00:00:00.000Z"
      }
    ],
    "pagination": {
      "page": 1,
      "limit": 10,
      "total": 25,
      "pages": 3
    }
  }
}
```

#### POST /tasks
Create a new task.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Request Body:**
```json
{
  "title": "Clean kitchen",
  "description": "Wipe counters and sweep floor",
  "priority": "medium",
  "category": "cleaning",
  "dueDate": "2024-01-15T00:00:00.000Z"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "task": {
      "id": "task-id",
      "title": "Clean kitchen",
      "description": "Wipe counters and sweep floor",
      "status": "pending",
      "priority": "medium",
      "category": "cleaning",
      "dueDate": "2024-01-15T00:00:00.000Z",
      "completedAt": null,
      "createdAt": "2024-01-01T00:00:00.000Z",
      "updatedAt": "2024-01-01T00:00:00.000Z"
    }
  }
}
```

#### GET /tasks/:id
Get a specific task by ID.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "task": {
      "id": "task-id",
      "title": "Clean kitchen",
      "description": "Wipe counters and sweep floor",
      "status": "pending",
      "priority": "medium",
      "category": "cleaning",
      "dueDate": "2024-01-15T00:00:00.000Z",
      "completedAt": null,
      "createdAt": "2024-01-01T00:00:00.000Z",
      "updatedAt": "2024-01-01T00:00:00.000Z"
    }
  }
}
```

#### PUT /tasks/:id
Update a task.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Request Body:**
```json
{
  "title": "Clean kitchen thoroughly",
  "description": "Wipe counters, sweep floor, and mop",
  "priority": "high",
  "status": "completed"
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "task": {
      "id": "task-id",
      "title": "Clean kitchen thoroughly",
      "description": "Wipe counters, sweep floor, and mop",
      "status": "completed",
      "priority": "high",
      "category": "cleaning",
      "dueDate": "2024-01-15T00:00:00.000Z",
      "completedAt": "2024-01-01T12:00:00.000Z",
      "createdAt": "2024-01-01T00:00:00.000Z",
      "updatedAt": "2024-01-01T12:00:00.000Z"
    }
  }
}
```

#### DELETE /tasks/:id
Delete a task.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Response:**
```json
{
  "success": true,
  "message": "Task deleted successfully"
}
```

#### PATCH /tasks/:id/complete
Mark a task as completed.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "task": {
      "id": "task-id",
      "status": "completed",
      "completedAt": "2024-01-01T12:00:00.000Z"
    }
  }
}
```

### Categories

#### GET /categories
Get all task categories.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Response:**
```json
{
  "success": true,
  "data": {
    "categories": [
      {
        "id": "category-id",
        "name": "Cleaning",
        "color": "#3B82F6",
        "icon": "broom"
      }
    ]
  }
}
```

#### POST /categories
Create a new category.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Request Body:**
```json
{
  "name": "Maintenance",
  "color": "#10B981",
  "icon": "wrench"
}
```

### Statistics

#### GET /stats
Get user statistics.

**Headers:**
```
Authorization: Bearer <jwt-token>
```

**Query Parameters:**
- `period` (string) - Time period (week, month, year)

**Response:**
```json
{
  "success": true,
  "data": {
    "totalTasks": 150,
    "completedTasks": 120,
    "pendingTasks": 30,
    "completionRate": 80,
    "averageCompletionTime": 2.5,
    "tasksByCategory": {
      "cleaning": 50,
      "maintenance": 30,
      "organization": 20
    },
    "tasksByPriority": {
      "high": 20,
      "medium": 80,
      "low": 50
    }
  }
}
```

## Error Codes

| Code | Description |
|------|-------------|
| `VALIDATION_ERROR` | Request data validation failed |
| `AUTHENTICATION_FAILED` | Invalid or missing authentication |
| `AUTHORIZATION_FAILED` | User doesn't have permission |
| `RESOURCE_NOT_FOUND` | Requested resource doesn't exist |
| `DUPLICATE_EMAIL` | Email already exists |
| `INVALID_CREDENTIALS` | Wrong email or password |
| `TOKEN_EXPIRED` | JWT token has expired |
| `RATE_LIMIT_EXCEEDED` | Too many requests |
| `INTERNAL_ERROR` | Server error |

## Rate Limiting

- **Authentication endpoints**: 5 requests per minute
- **Other endpoints**: 100 requests per minute

Rate limit headers are included in responses:
```
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 95
X-RateLimit-Reset: 1640995200
```

## Webhooks

Webhooks can be configured to receive real-time updates:

#### POST /webhooks
Configure webhook endpoints.

**Request Body:**
```json
{
  "url": "https://your-app.com/webhook",
  "events": ["task.created", "task.completed"],
  "secret": "webhook-secret"
}
```

Webhook payload example:
```json
{
  "event": "task.completed",
  "timestamp": "2024-01-01T12:00:00.000Z",
  "data": {
    "task": {
      "id": "task-id",
      "title": "Clean kitchen",
      "status": "completed"
    }
  }
}
```

## SDKs and Libraries

### JavaScript/TypeScript
```bash
npm install housekeeping-journal-sdk
```

```typescript
import { HousekeepingJournalAPI } from 'housekeeping-journal-sdk';

const api = new HousekeepingJournalAPI({
  baseURL: 'https://api.housekeeping-journal.com',
  token: 'your-jwt-token'
});

const tasks = await api.tasks.list();
```

## Support

For API support:
- **Email**: api-support@housekeeping-journal.com
- **Documentation**: https://docs.housekeeping-journal.com
- **Status Page**: https://status.housekeeping-journal.com 