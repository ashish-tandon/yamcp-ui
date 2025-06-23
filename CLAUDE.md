# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

YAMCP UI is a web-based dashboard for YAMCP (Yet Another MCP) - A Model Context Protocol workspace manager. It provides a React frontend with an Express.js backend server that integrates with the YAMCP CLI tool.

## Architecture

### Frontend (React + TypeScript)
- **Framework**: React 18 with TypeScript, built with Vite
- **Styling**: Tailwind CSS with custom design system
- **UI Components**: Radix UI primitives with custom shadcn/ui components
- **Routing**: React Router DOM for SPA navigation
- **State Management**: Local component state with React hooks
- **Charts**: Recharts for data visualization

### Backend (Express.js)
- **Server**: Express.js server in `server.mjs`
- **Integration**: Dynamically imports YAMCP modules from global installation
- **Security**: CORS protection, localhost-only access
- **API**: RESTful endpoints for server/workspace management
- **File Operations**: Direct JSON file manipulation for configuration

### Key Architecture Patterns
- **Pages**: Main application views in `src/pages/` (Dashboard, Servers, Workspaces, Logs, Settings)
- **Components**: Reusable UI components in `src/components/` with ui/ subfolder for base components
- **Layout**: Single layout component with responsive sidebar navigation
- **API Integration**: Frontend communicates with Express backend via `/api/*` endpoints
- **Configuration**: YAMCP stores configuration in JSON files (providers.json, workspaces.json)

## Development Commands

```bash
# Install dependencies
npm install

# Development server (frontend only, requires separate backend)
npm run dev

# Build for production
npm run build

# Start production server (includes both frontend and backend)
npm start

# Preview built application
npm preview

# Prepare for publishing
npm run prepublishOnly
```

## Development Workflow

1. **Frontend Development**: Use `npm run dev` for hot-reload development
2. **Full Application Testing**: Use `npm run build && node bin/yamcp-ui.js` for complete testing
3. **Testing Changes**: As per Cursor rules, after UI changes run build → start server → test with Playwright on port 8765

## Key Files and Structure

- `server.mjs` - Express backend server with YAMCP integration and API endpoints
- `src/App.tsx` - Main React application with routing setup
- `src/components/Layout.tsx` - Main layout with responsive sidebar navigation
- `src/pages/` - Main application pages (Dashboard, Servers, Workspaces, Logs, Settings)
- `src/components/ui/` - Base UI components (shadcn/ui style)
- `src/contexts/ThemeContext.tsx` - Theme management for dark/light mode
- `bin/yamcp-ui.js` - CLI entry point script

## YAMCP Integration

The application integrates with YAMCP through:
- **Dynamic Module Loading**: Server imports YAMCP modules at runtime
- **Configuration Files**: Direct manipulation of YAMCP's JSON configuration files
- **Log File Reading**: Accesses YAMCP log files for monitoring
- **Provider Management**: CRUD operations on MCP providers/servers
- **Workspace Management**: CRUD operations on YAMCP workspaces

## API Endpoints

- `GET /api/stats` - Dashboard statistics
- `GET /api/servers` - List MCP servers/providers
- `GET /api/workspaces` - List workspaces
- `GET /api/logs` - Recent log entries
- `POST/PUT/DELETE /api/servers/*` - Server management
- `POST/PUT/DELETE /api/workspaces/*` - Workspace management
- `GET /api/config/*` - Raw JSON configuration access

## Security Considerations

- Backend restricts API access to localhost only
- CORS configured for same-origin requests
- No external network access required
- Configuration files accessed securely through YAMCP integration

## Code Style Notes

- Do not import React unless explicitly using React-specific features (JSX transform handles JSX)
- Use TypeScript interfaces for type safety
- Follow Tailwind CSS utility-first approach
- Use Radix UI primitives for accessible components
- Maintain consistent file naming and structure conventions