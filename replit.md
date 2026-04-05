# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)
- **Real-time**: Socket.IO (server + client)

## Artifacts

### Müzik Chat (`artifacts/music-chat`)
- Real-time multi-room music chat platform
- React + Vite frontend at `/`
- Socket.IO for real-time communication
- YouTube IFrame API for synchronized playback
- Features: multi-room chat, YouTube music sync, queue system, live user list
- All UI in Turkish

### API Server (`artifacts/api-server`)
- Express 5 backend at `/api`
- Socket.IO server at `/socket.io` 
- In-memory room state (rooms, users, playback, chat history, queue)
- No database needed — stateless rooms that persist while users are present

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally
- `pnpm --filter @workspace/music-chat run dev` — run music chat frontend

## Socket.IO Events

### Client → Server
- `join-room` — join a named room with a nickname
- `send-message` — send a chat message (auto-detects YouTube URLs)
- `add-to-queue` — explicitly add YouTube URL to queue
- `skip-song` — skip current song
- `pause-playback` — pause for all in room
- `resume-playback` — resume for all in room
- `remove-from-queue` — remove item from queue
- `reorder-queue` — drag-and-drop queue reordering
- `clear-queue` — clear the queue
- `song-ended` — notify server song ended (triggers next song)
- `request-sync` — request current playback state

### Server → Client
- `room-list` — updated list of all rooms
- `room-joined` — full room state on join
- `user-list` — updated list of users in room
- `chat-message` — new chat message
- `playback-update` — playback state change
- `queue-update` — queue state change

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.
