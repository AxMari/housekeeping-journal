# Housekeeping Journal

A smart, responsive housekeeping calendar application built with Next.js, React, TypeScript, and Tailwind CSS. Features a professional calendar interface with task management capabilities and mobile-first design.

## 🚀 Features

- **Smart Calendar Interface**: Professional time-based calendar with multiple views
- **Task Library**: Comprehensive task management system
- **Professional Services Integration**: Connect with housekeeping services
- **Responsive Design**: Mobile-first approach with desktop optimization
- **PWA Support**: Progressive Web App capabilities for app-like experience
- **Modern UI**: Clean, intuitive interface with Tailwind CSS styling

## 🛠️ Tech Stack

- **Frontend**: Next.js 15, React 18, TypeScript
- **Styling**: Tailwind CSS v4
- **Calendar**: react-big-calendar
- **Testing**: Jest
- **Build Tool**: Turbopack
- **Package Manager**: npm

## 📱 Platform Support

- **Mobile**: Optimized for iOS and Android with PWA support
- **Desktop**: Responsive web interface for desktop users
- **Hybrid**: App-like experience with website accessibility

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ 
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd housekeeping-journal
   ```

2. **Install dependencies**
   ```bash
   cd frontend
   npm install
   ```

3. **Start the development server**
   ```bash
   npm run dev
   ```

4. **Open your browser**
   - Local: http://localhost:3000
   - Network: http://192.168.1.151:3000 (for mobile testing)

### Development Commands

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm start

# Run tests
npm test

# Run tests in watch mode
npm run test:watch
```

## 📁 Project Structure

```
housekeeping-journal/
├── frontend/                 # Next.js application
│   ├── src/
│   │   ├── app/             # App router pages
│   │   ├── components/      # React components
│   │   └── __tests__/       # Test files
│   ├── public/              # Static assets
│   └── package.json
├── backend/                 # Backend API (future)
├── shared/                  # Shared utilities (future)
├── docs/                    # Documentation
└── README.md
```

## 🎨 UI Components

### Calendar
- **Time-based view**: Hourly scheduling with professional styling
- **Responsive grid**: Adapts between mobile and desktop layouts
- **Custom styling**: Extensive CSS overrides for react-big-calendar
- **Selection highlighting**: Interactive time slot selection

### Navigation
- **Mobile-first**: Bottom navigation for mobile devices
- **Desktop adaptation**: Top navigation for desktop users
- **Responsive breakpoints**: Smooth transitions between layouts

### Task Library
- **Comprehensive task management**: Add, edit, and organize tasks
- **Category system**: Organize tasks by room, frequency, or type
- **Professional integration**: Connect with housekeeping services

## 🔧 Configuration

### Tailwind CSS
The project uses Tailwind CSS v4 with custom configuration for optimal styling and responsive design.

### Calendar Styling
Extensive custom CSS overrides ensure the calendar maintains professional appearance across all devices and screen sizes.

## 📱 Mobile Development

### PWA Features
- Service worker for offline functionality
- App-like installation experience
- Responsive design optimized for touch interactions

### Mobile Testing
- Use the network URL to test on mobile devices
- Ensure proper touch targets (44px minimum)
- Test responsive breakpoints

## 🧪 Testing

The project includes Jest configuration for unit and integration testing:

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Generate coverage report
npm run test:coverage
```

## 🚀 Deployment

### Vercel (Recommended)
1. Connect your GitHub repository to Vercel
2. Configure build settings:
   - Build Command: `cd frontend && npm run build`
   - Output Directory: `frontend/.next`
3. Deploy automatically on push to main branch

### Other Platforms
The Next.js app can be deployed to any platform that supports Node.js applications.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🆘 Support

For support and questions:
- Create an issue in the GitHub repository
- Check the documentation in the `/docs` folder
- Review the component examples in `/src/components`

## 🔮 Roadmap

- [ ] Backend API development
- [ ] User authentication
- [ ] Database integration
- [ ] Real-time notifications
- [ ] Advanced task scheduling
- [ ] Service provider marketplace
- [ ] Analytics and reporting
- [ ] Multi-language support
