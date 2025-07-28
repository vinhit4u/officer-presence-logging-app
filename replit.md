# Replit.md

## Overview

This is a full-stack TypeScript application for an officer presence logging system. It's built with a React frontend using shadcn/ui components and a Node.js/Express backend with PostgreSQL database integration through Drizzle ORM. The application features Replit-based authentication and geolocation-based presence tracking.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **UI Library**: shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **Routing**: Wouter for client-side routing
- **State Management**: TanStack Query (React Query) for server state
- **Forms**: React Hook Form with Zod validation
- **Build Tool**: Vite with custom configuration for monorepo structure

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Authentication**: Replit OpenID Connect (OIDC) integration
- **Session Management**: express-session with PostgreSQL store
- **Database Connection**: Neon serverless PostgreSQL

### Project Structure
```
├── client/          # React frontend
├── server/          # Express backend
├── shared/          # Shared types and schemas
└── migrations/      # Database migrations
```

## Key Components

### Authentication System
- **Provider**: Replit OIDC authentication
- **Implementation**: Passport.js strategy with OpenID Client
- **Session Storage**: PostgreSQL-based session store using connect-pg-simple
- **User Management**: Automatic user creation/update on login

### Database Schema
- **users**: User profiles with employee information
- **sessions**: Session storage for authentication
- **presence_logs**: Geolocation-based attendance tracking

### Frontend Pages
- **Landing**: Authentication entry point
- **Dashboard**: Main interface for presence logging
- **Profile**: User profile management
- **Not Found**: 404 error handling

### Core Features
- **Location Capture**: Browser geolocation API integration
- **Presence Logging**: Timestamped location-based attendance
- **Profile Management**: Employee information updates
- **Real-time UI**: Toast notifications and loading states
- **Official Branding**: PKD and Kerala State Police logos integrated across all pages

## Data Flow

1. **Authentication Flow**:
   - User accesses application → Redirected to Replit OIDC
   - Successful auth → User profile created/updated
   - Session established → Access to protected routes

2. **Presence Logging Flow**:
   - User grants location permission
   - Continuous location tracking when active
   - Manual presence log creation with coordinates
   - Server validation and database storage

3. **Profile Management**:
   - User updates profile information
   - Form validation with Zod schemas
   - Optimistic UI updates with React Query

## External Dependencies

### Core Dependencies
- **Database**: Neon PostgreSQL serverless
- **Authentication**: Replit OIDC service
- **UI Framework**: Radix UI primitives
- **Validation**: Zod for runtime type checking
- **HTTP Client**: Native fetch with custom wrapper

### Development Tools
- **Build**: Vite for frontend, esbuild for backend
- **Type Checking**: TypeScript with strict configuration
- **CSS**: Tailwind CSS with PostCSS processing
- **Code Quality**: ESLint and Prettier (implied)

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds React app to `dist/public`
- **Backend**: esbuild bundles server to `dist/index.js`
- **Database**: Drizzle migrations applied via `db:push`

### Environment Requirements
- `DATABASE_URL`: PostgreSQL connection string
- `SESSION_SECRET`: Session encryption key
- `REPL_ID`: Replit application identifier
- `ISSUER_URL`: OIDC issuer endpoint (defaults to Replit)
- `REPLIT_DOMAINS`: Allowed domains for OIDC

### Production Considerations
- Session cookies configured for HTTPS
- Database connection pooling via Neon
- Error handling with proper HTTP status codes
- CORS and security headers (implicit)

### Development vs Production
- **Development**: Hot reload with Vite middleware
- **Production**: Static file serving from Express
- **Database**: Same PostgreSQL setup for both environments

## Recent Updates (January 28, 2025)

### Technical Fixes
- **Database Schema**: Fixed GPS accuracy overflow error by increasing decimal precision from (6,2) to (10,2)
- **TypeScript**: Resolved all LSP diagnostics with proper type definitions for User and PresenceLog types
- **Presence Logging**: Confirmed GPS location capture and database storage working correctly

### UI Enhancements  
- **Official Branding**: Integrated PKD and Kerala State Police logos across all pages
- **Logo Placement**: Added logos to landing page, dashboard header, and profile page header
- **Professional Appearance**: Enhanced visual identity with official police insignia

### Functionality Status
- ✅ User authentication with Replit Auth working
- ✅ GPS location capture and accuracy tracking working  
- ✅ Presence logging with timestamp and coordinates working
- ✅ Officer profile management working
- ✅ Database persistence and retrieval working