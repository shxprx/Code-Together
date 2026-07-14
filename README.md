# CodeTogether 🚀

> A real-time collaborative code editor where multiple users can join the same room, edit code simultaneously, and securely compile & execute programs inside isolated Docker containers.

Designed as a backend-focused project to demonstrate **WebSockets, Docker sandboxing, concurrency handling, scalable architecture, and clean software design.**

---

# ✨ Features

### Collaboration

- Real-time collaborative editing
- Shareable Room IDs
- Live participant list
- Instant language synchronization
- Shared execution output
- Automatic room cleanup

### Code Execution

- C++
- Python
- Java
- Docker-based sandbox
- Standard input support
- Compilation output
- Runtime output

### Security

- Docker isolation
- No network access
- Filesystem isolation
- CPU & memory limits
- Execution timeout
- Process limits
- Input validation

---

# 🏗 System Architecture

```
                Browser
                    │
        HTTP + WebSocket
                    │
                    ▼
          React + Monaco Editor
                    │
                    ▼
             Express Backend
      ┌────────────┼─────────────┐
      │            │             │
      ▼            ▼             ▼
 RoomManager   WebSocket   REST APIs
      │
      ▼
 Executor Registry
      │
 ┌────┼────┐
 ▼    ▼    ▼
C++ Python Java
      │
      ▼
 Docker Containers
```

---

# Tech Stack

### Frontend

- React
- Vite
- Monaco Editor
- Context API
- Vanilla CSS

### Backend

- Node.js
- Express.js
- WebSocket (ws)

### Infrastructure

- Docker
- Docker Images
- Temporary Workspace

---

# Key Engineering Concepts

This project demonstrates practical implementation of

- WebSocket Communication
- Real-time Systems
- Event-driven Architecture
- Clean Architecture
- SOLID Principles
- Strategy Pattern
- Singleton Pattern
- Resource Isolation
- Secure Code Execution
- Backend State Management
- Concurrency Control
- REST API Design

---

# Project Structure

```
backend/

├── core/
│     RoomManager
│     Room
│     Participant
│
├── websocket/
│     wsServer
│     wsHandlers
│
├── executors/
│     ExecutorRegistry
│     CppExecutor
│     PythonExecutor
│     JavaExecutor
│
├── routes/
│
├── utils/
│
└── server.js


frontend/

├── components/
├── hooks/
├── context/
├── services/
└── App.jsx
```

---

# Execution Flow

```
User Types Code
        │
        ▼
WebSocket Broadcast
        │
        ▼
RoomManager Updates State
        │
        ▼
All Participants Receive Update
        │
        ▼
Run Code
        │
        ▼
Executor Registry
        │
        ▼
Language Executor
        │
        ▼
Docker Container
        │
        ▼
Compilation
        │
        ▼
Execution
        │
        ▼
Broadcast Output
```

---

# API Overview

| Method | Endpoint | Description |
|---------|----------|-------------|
| POST | /api/rooms | Create Room |
| POST | /api/run | Execute Code |
| GET | /api/health | Health Check |

---

# WebSocket Events

### Client → Server

- JOIN_ROOM
- CODE_CHANGE
- LANGUAGE_CHANGE
- LEAVE_ROOM

### Server → Client

- ROOM_STATE
- USER_JOINED
- USER_LEFT
- CODE_UPDATED
- LANGUAGE_UPDATED
- OUTPUT_UPDATED
- ERROR

---

# Security

- Docker sandbox for every execution
- Fresh container per compilation
- No shared filesystem
- No internet access
- CPU limits
- Memory limits
- PID limits
- Execution timeout
- Input validation
- Backend-owned room state

---

# Concurrency Handling

The backend acts as the **single source of truth**.

To avoid race conditions:

- Only one compilation can run per room
- Backend owns room state
- WebSocket messages are validated
- RoomManager synchronizes all updates
- Empty rooms are automatically cleaned up

---

# Design Patterns

| Pattern | Usage |
|----------|------|
| Singleton | RoomManager |
| Strategy | Executor Registry |
| Registry | Language Executors |
| Modular Architecture | Backend Modules |
| Event-driven | WebSocket Communication |

---

# Scalability

Current

- Single backend server
- In-memory room state

Future Improvements

- Redis Pub/Sub
- BullMQ
- Persistent Database
- JWT Authentication
- Horizontal Scaling
- CRDT / OT
- Cursor Synchronization
- Multi-file Projects
- Team Workspaces
- Chat

---

# Local Setup

Clone repository

```bash
git clone https://github.com/username/codetogether.git
```

Backend

```bash
cd backend
npm install
npm run dev
```

Frontend

```bash
cd frontend
npm install
npm run dev
```

Build Docker Images

```bash
docker build -t code-executor-cpp backend/docker/cpp

docker build -t code-executor-python backend/docker/python

docker build -t code-executor-java backend/docker/java
```



# Screenshots

> Add screenshots here.

- Home Page
- Editor
- Multiple Participants
- Shared Output
- Docker Execution

---

# Future Roadmap

- Authentication
- Persistent Rooms
- Redis
- Multi-server Support
- Chat
- Presence Indicators
- Cursor Tracking
- File Tree
- Project Templates
- Execution Queue

---

# License

MIT License.
