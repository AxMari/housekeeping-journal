# Development Guide

This guide provides detailed information for developers working on the Housekeeping Journal project.

## 🏗 Architecture Overview

The project follows a modern, scalable architecture:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   Database      │
│   (Next.js)     │◄──►│   (Node.js)     │◄──►│   (PostgreSQL)  │
│                 │    │                 │    │                 │
│ - React 19      │    │ - Express.js    │    │ - Prisma ORM    │
│ - TypeScript    │    │ - TypeScript    │    │ - Migrations    │
│ - Tailwind CSS  │    │ - JWT Auth      │    │ - Seeding       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

## 📁 Directory Structure

### Frontend (`/frontend`)
```
src/
├── app/                    # Next.js App Router
│   ├── layout.tsx         # Root layout
│   ├── page.tsx           # Home page
│   └── globals.css        # Global styles
├── components/            # Reusable components
│   ├── ui/               # Basic UI components
│   ├── forms/            # Form components
│   └── layout/           # Layout components
├── lib/                  # Utility functions
│   ├── utils.ts          # General utilities
│   ├── api.ts            # API client
│   └── auth.ts           # Authentication
├── types/                # TypeScript definitions
│   ├── api.ts            # API types
│   ├── components.ts     # Component props
│   └── global.ts         # Global types
└── __tests__/            # Test files
    ├── setup.tsx         # Test configuration
    ├── test-utils.tsx    # Testing utilities
    └── components/       # Component tests
```

### Backend (`/backend`) - Planned
```
src/
├── controllers/          # Route handlers
├── middleware/           # Custom middleware
├── models/              # Data models
├── routes/              # API routes
├── services/            # Business logic
├── utils/               # Utility functions
└── types/               # TypeScript types
```

### Shared (`/shared`)
```
types/                   # Shared TypeScript types
constants/               # Shared constants
utils/                   # Shared utilities
```

## 🛠 Development Setup

### Prerequisites
- Node.js 18+ 
- npm or yarn
- Git
- VS Code (recommended)

### VS Code Extensions
```json
{
  "recommendations": [
    "bradlc.vscode-tailwindcss",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint",
    "ms-vscode.vscode-typescript-next",
    "formulahendry.auto-rename-tag",
    "christian-kohler.path-intellisense"
  ]
}
```

### Environment Variables

#### Frontend (`.env.local`)
```env
# App Configuration
NEXT_PUBLIC_APP_NAME=Housekeeping Journal
NEXT_PUBLIC_APP_VERSION=1.0.0

# API Configuration
NEXT_PUBLIC_API_URL=http://localhost:3001
NEXT_PUBLIC_API_TIMEOUT=10000

# Feature Flags
NEXT_PUBLIC_ENABLE_ANALYTICS=false
NEXT_PUBLIC_ENABLE_DEBUG=true
```

#### Backend (`.env`) - Planned
```env
# Server Configuration
PORT=3001
NODE_ENV=development

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/housekeeping

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=7d

# CORS
CORS_ORIGIN=http://localhost:3000
```

## 🔧 Development Workflow

### 1. Feature Development

```bash
# Create feature branch
git checkout -b feature/task-management

# Install dependencies (if needed)
npm install

# Start development server
npm run dev

# Run tests in watch mode
npm run test:watch
```

### 2. Code Quality

```bash
# Lint code
npm run lint

# Fix linting issues
npm run lint:fix

# Format code
npm run format

# Type check
npm run type-check
```

### 3. Testing

```bash
# Run all tests
npm test

# Run tests with coverage
npm run test:coverage

# Run specific test file
npm test -- TaskList.test.tsx

# Run tests matching pattern
npm test -- --grep "TaskList"
```

### 4. Building

```bash
# Build for production
npm run build

# Start production server
npm run start

# Analyze bundle
npm run analyze
```

## 📝 Coding Standards

### TypeScript
- Use strict mode
- Prefer interfaces over types for objects
- Use proper typing for all functions
- Avoid `any` type

```typescript
// ✅ Good
interface Task {
  id: string;
  title: string;
  completed: boolean;
  createdAt: Date;
}

const createTask = (title: string): Task => ({
  id: generateId(),
  title,
  completed: false,
  createdAt: new Date(),
});

// ❌ Bad
const createTask = (title: any): any => ({
  id: generateId(),
  title,
  completed: false,
  createdAt: new Date(),
});
```

### React Components
- Use functional components with hooks
- Prefer composition over inheritance
- Use proper prop typing
- Keep components focused and small

```typescript
// ✅ Good
interface TaskItemProps {
  task: Task;
  onToggle: (id: string) => void;
  onDelete: (id: string) => void;
}

export const TaskItem: React.FC<TaskItemProps> = ({
  task,
  onToggle,
  onDelete,
}) => {
  return (
    <div className="flex items-center gap-2 p-2 border rounded">
      <input
        type="checkbox"
        checked={task.completed}
        onChange={() => onToggle(task.id)}
      />
      <span className={task.completed ? 'line-through' : ''}>
        {task.title}
      </span>
      <button onClick={() => onDelete(task.id)}>Delete</button>
    </div>
  );
};
```

### CSS/Styling
- Use Tailwind CSS classes
- Follow mobile-first approach
- Use semantic class names
- Avoid custom CSS when possible

```typescript
// ✅ Good
<div className="flex flex-col gap-4 p-6 bg-white rounded-lg shadow-md">
  <h2 className="text-xl font-semibold text-gray-900">Task List</h2>
  <div className="space-y-2">
    {tasks.map(task => (
      <TaskItem key={task.id} task={task} />
    ))}
  </div>
</div>

// ❌ Bad
<div className="task-container">
  <h2 className="task-title">Task List</h2>
  <div className="task-list">
    {tasks.map(task => (
      <TaskItem key={task.id} task={task} />
    ))}
  </div>
</div>
```

## 🧪 Testing Guidelines

### Component Testing
- Test user interactions
- Test accessibility
- Test error states
- Test loading states

```typescript
describe('TaskItem', () => {
  it('toggles completion when checkbox is clicked', async () => {
    const user = userEvent.setup();
    const mockToggle = jest.fn();
    
    render(
      <TaskItem
        task={{ id: '1', title: 'Test Task', completed: false }}
        onToggle={mockToggle}
        onDelete={jest.fn()}
      />
    );
    
    const checkbox = screen.getByRole('checkbox');
    await user.click(checkbox);
    
    expect(mockToggle).toHaveBeenCalledWith('1');
  });
});
```

### API Testing
- Mock external dependencies
- Test success and error cases
- Test loading states
- Test data transformations

### Accessibility Testing
- Test keyboard navigation
- Test screen reader compatibility
- Test color contrast
- Test focus management

## 🔍 Debugging

### Frontend Debugging
```typescript
// Use React DevTools
// Use browser DevTools
// Use console.log strategically
console.log('Task data:', tasks);

// Use React Query DevTools (if using)
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';
```

### Backend Debugging
```typescript
// Use debug logging
import debug from 'debug';
const log = debug('app:api');

log('Processing request:', req.body);

// Use proper error handling
try {
  const result = await processData(data);
  return res.json(result);
} catch (error) {
  log('Error processing data:', error);
  return res.status(500).json({ error: 'Internal server error' });
}
```

## 🚀 Performance

### Frontend Optimization
- Use React.memo for expensive components
- Implement proper loading states
- Use image optimization
- Implement code splitting

```typescript
// Code splitting
const TaskList = lazy(() => import('./TaskList'));

// Memoization
const ExpensiveComponent = React.memo(({ data }) => {
  return <div>{/* Expensive rendering */}</div>;
});
```

### Backend Optimization
- Implement caching
- Use database indexing
- Implement pagination
- Use connection pooling

## 🔒 Security

### Frontend Security
- Validate user input
- Sanitize data
- Use HTTPS in production
- Implement proper CORS

### Backend Security
- Validate all inputs
- Use parameterized queries
- Implement rate limiting
- Use proper authentication
- Sanitize user data

## 📊 Monitoring

### Frontend Monitoring
- Error tracking (Sentry)
- Performance monitoring
- User analytics
- A/B testing

### Backend Monitoring
- Application performance
- Database performance
- Error tracking
- Health checks

## 🚀 Deployment

### Frontend Deployment
1. Build the application
2. Run tests
3. Deploy to platform
4. Verify deployment

### Backend Deployment
1. Run database migrations
2. Deploy application
3. Run health checks
4. Monitor logs

## 📚 Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [React Documentation](https://react.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [Testing Library Documentation](https://testing-library.com/docs)

---

**Remember**: Write clean, maintainable code that others can understand and build upon. 