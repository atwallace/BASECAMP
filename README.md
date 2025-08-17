# BASECAMP

## Overview

A comprehensive web application to manage command picnic rental requests for Morale Welfare & Recreation (MWR) services. This system replaces the current whiteboard-based tracking with a digital solution that enforces business rules, prevents double-booking, and provides real-time tracking of gear pickup/returns.

## Problem Statement

Currently, command picnic requests are tracked on a whiteboard system which leads to:
- Lost or misplaced requests
- Double booking of events
- Difficulty tracking gear utilization
- Manual enforcement of program rules
- Poor visibility into request status

## Solution

A Next.js web application with dual interfaces:
- **Staff Portal**: Manage requests, track gear, enforce compliance rules
- **Command Portal**: Submit requests online, track status, view pickup/return progress

## Key Features

### Request Management
- Online request submission with automatic validation
- 10-day advance notice requirement enforcement
- Dual-stage approval process (initial request + command letter)
- Calendar-based scheduling with conflict prevention

### Compliance Enforcement
- Maximum 1 command per day, 2 per week (with override capability)
- Once per calendar year limit per command
- Base-only command verification system
- Automatic rule validation

### Real-Time Tracking
- Live pickup/return status updates
- Partial gear fulfillment tracking
- Outstanding items monitoring
- Staff annotation system for multiple trips

### Reporting & Analytics
- Gear utilization reporting
- Command usage analytics
- Annual compliance summaries
- Staff workload distribution

## Tech Stack

- **Frontend**: Next.js 15, React 19, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: PostgreSQL
- **Real-time**: Server-Sent Events (SSE)
- **Authentication**: NextAuth.js
- **Deployment**: Vercel

## Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL 14+
- pnpm

### Installation

1. Clone the repository
```bash
git clone https://github.com/atwallace/basecamp.git
cd basecamp
```

2. Install dependencies
```bash
pnpm install
```

3. Set up environment variables
```bash
cp .env.example .env.local
# Edit .env.local with your database and auth settings
```

4. Set up the database
```bash
pnpm run db:migrate
pnpm run db:seed
```

5. Start the development server
```bash
pnpm run dev
```

Visit `http://localhost:3000` to access the application.

## Project Structure

```
mwr-rental-management/
├── app/                   # Next.js 15 app directory
│   ├── staff/             # Staff portal pages
│   ├── command/           # Command portal pages
│   ├── api/               # API routes
│   └── globals.css        # Global styles
├── components/            # Reusable React components
├── lib/                   # Utilities and configurations
│   ├── db.ts              # Database connection
│   ├── auth.ts            # Authentication setup
│   └── validations.ts     # Request validation rules
├── types/                 # TypeScript type definitions
├── prisma/                # Database schema and migrations
├── public/                # Static assets
└── docs/                  # Additional documentation
```

## Environment Variables

Required environment variables (see `.env.example`):

```
DATABASE_URL=postgresql://username:password@localhost:5432/basecamp
NEXTAUTH_SECRET=your-secret-key
NEXTAUTH_URL=http://localhost:3000
```

## Database Schema

Key entities:
- **Commands**: Verified base commands
- **Requests**: Picnic rental requests
- **GearItems**: Available rental inventory
- **RequestItems**: Specific gear requested with quantities
- **PickupReturns**: Tracking of gear movement

## API Endpoints

### Staff Endpoints
- `GET /api/staff/requests` - List all requests
- `POST /api/staff/requests/:id/approve` - Approve request
- `PUT /api/staff/requests/:id/gear` - Update pickup/return status

### Command Endpoints
- `POST /api/commands/register` - Request command verification
- `POST /api/commands/requests` - Submit new request
- `GET /api/commands/requests` - View own requests

### Real-time Endpoints
- `GET /api/updates/stream` - Server-sent events for live updates

## Development

### Running Tests
```bash
pnpm run test              # Unit tests
pnpm run test:e2e         # End-to-end tests
pnpm run test:coverage    # Coverage report
```

### Code Quality
```bash
pnpm run lint             # ESLint
pnpm run type-check       # TypeScript validation
pnpm run format           # Prettier formatting
```

### Database Management
```bash
pnpm run db:migrate       # Run migrations
pnpm run db:seed          # Seed test data
pnpm run db:reset         # Reset database
pnpm run db:studio        # Open Prisma Studio
```

## Deployment

### Docker Deployment
```bash
docker build -t mwr-rental-management .
docker run -p 3000:3000 --env-file .env.production mwr-rental-management
```

### Environment Setup
Ensure proper environment variables are set for production deployment.

## Security Considerations

- Command verification required before system access
- Base-only access enforcement
- Request validation and sanitization
- Audit logging for all staff actions
- Rate limiting on API endpoints

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## Support

For technical issues or feature requests, please create an issue in the GitHub repository.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and updates.