# SkillSwap MVP

## Overview
SkillSwap is a peer-to-peer skill exchange platform where users can teach what they know and learn what they want. The application features AI-powered matching with explainable recommendations, profile management, and session scheduling.

## Tech Stack
- **Frontend**: React 18 + TypeScript + Tailwind CSS + Vite
- **Backend**: Express.js + TypeScript
- **Styling**: Tailwind CSS with dark glass theme, shadcn/ui components
- **State Management**: TanStack Query for server state
- **Routing**: Wouter
- **Authentication**: JWT in httpOnly cookies + bcrypt password hashing

## Project Structure
```
client/
├── src/
│   ├── components/
│   │   ├── ui/              # shadcn components
│   │   ├── auth-context.tsx # Auth state provider
│   │   ├── auth-modal.tsx   # Login/register modal
│   │   ├── loading-skeleton.tsx
│   │   ├── mode-badge.tsx   # ONLINE/OFFLINE badge
│   │   ├── navigation.tsx   # Top nav bar
│   │   ├── reputation-badge.tsx
│   │   ├── skill-chip.tsx   # Skill display with level
│   │   └── theme-provider.tsx
│   ├── pages/
│   │   ├── home.tsx         # Landing page
│   │   ├── not-found.tsx
│   │   ├── profile.tsx      # Profile management
│   │   ├── recommendations.tsx # Top-5 matches with XAI
│   │   └── schedule.tsx     # Session booking
│   ├── hooks/
│   ├── lib/
│   │   └── queryClient.ts   # API helpers
│   └── App.tsx

server/
├── middleware/
│   └── auth.ts              # JWT verification
├── utils/
│   ├── fuzzy.ts             # Skill matching (synonyms, trigrams)
│   └── xai.ts               # XAI explanation generator
├── index.ts                 # Express server entry
├── routes.ts                # All API endpoints
├── seed.ts                  # Seed data (5 users, 12 skills)
└── storage.ts               # In-memory storage implementation

shared/
└── schema.ts                # Drizzle schema + Zod validators + Types
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Create new user account
- `POST /api/auth/login` - Login and set JWT cookie
- `POST /api/auth/logout` - Clear auth cookie
- `GET /api/auth/me` - Get current user with profile

### Profile
- `GET /api/profile/me` - Get user's profile with details
- `PUT /api/profile/me` - Update profile, skills, availability
- `GET /api/profile/:id` - Get specific profile

### Skills
- `GET /api/skills` - List all available skills

### Matching
- `GET /api/matching/top` - Get Top-5 personalized recommendations
- `POST /api/matching/accept` - Accept a match

### Scheduling
- `POST /api/schedule` - Create a session booking

## Features

### AI-Powered Matching
The matching algorithm uses:
1. **Mock embeddings**: Deterministic pseudo-vectors from skill names
2. **Synonym matching**: Maps related skills (e.g., "Python Basics" ≈ "Intro to Python")
3. **Fuzzy matching**: Trigram similarity for tolerant term matching (threshold ≥ 0.75)
4. **Multi-factor reranking**: Combines skill similarity, time overlap, reputation, freshness

### XAI Explanations
Each recommendation includes a human-readable explanation:
- Matched skills
- Overlapping time slots
- Reputation score

### Profile Management
- Display name and bio
- Offered skills with proficiency levels (1-5)
- Wanted skills
- Weekly availability with time slots
- Visibility settings (Public/Limited/Private)

### Session Scheduling
- Date and time selection
- Online/In-person mode toggle
- Optional notes
- Reminder preferences (24h, 2h before)

## Seed Data
The application starts with:
- 12 skills across programming, data, design, and soft skills
- 5 users with complete profiles, skills, availability, and reputation
- Sample users: Ana M., Boris K., Carla D., David L., Elena S.

## Development

### Running the App
```bash
npm run dev
```
Starts both frontend (Vite) and backend (Express) on port 5000.

### Test Accounts
Use any seeded account with password `password123`:
- ana@example.com
- boris@example.com
- carla@example.com
- david@example.com
- elena@example.com

## Recent Changes
- Initial MVP implementation (December 2025)
- Dark glass theme with purple/violet accents
- Full auth flow with JWT cookies
- Profile management with skills and availability
- AI-powered matching with XAI explanations
- Session scheduling with reminders

## Design Preferences
- Dark mode by default
- Glass morphism aesthetic
- Purple/violet primary colors
- Clean card-based layouts
- Subtle hover animations using built-in elevation system
