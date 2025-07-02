# PostgreSQL Real-Time Monitoring Dashboard – Copilot Development Writeup

## Overview
Build a real-time PostgreSQL monitoring dashboard with the following features:
- Real-time and historical monitoring of PostgreSQL server metrics (CPU, replication lag, blocking queries, etc.)
- Data is collected from multiple servers using a credential file
- Frontend in React.js (with Recharts for graphs)
- Backend in Node.js/Express (with Socket.IO for real-time updates)
- Data is stored in a central database for historical queries

---

## Architecture

**Frontend:**
- React.js (functional components, hooks)
- Recharts for data visualization
- Responsive dashboard layout
- UI allows:
  - Selecting a server from a dropdown (populated from backend credential file)
  - Manual entry fallback for connection details
  - Real-time mode (live updates via WebSocket)
  - Historical mode (user enters hostname and date range, fetches from backend DB)
  - Tabbed interface for CPU, Replication, Blocking, and Query Console
  - Download CSV for all tables

**Backend:**
- Node.js with Express
- Socket.IO for WebSocket communication
- Reads a credential file (JSON or similar) for server connection info
- Polls each server every 5 seconds for metrics:
  - Uses `pg_stat_statements` for query performance
  - Uses `pg_stat_replication` for replication metrics
  - Uses `pg_locks` for blocking query detection
  - Collects OS metrics (CPU, memory, etc.) via agent or SSH (if possible)
- Stores all collected metrics in a central PostgreSQL database for historical queries
- Exposes REST endpoints:
  - `/api/servers` – returns list of servers from credential file
  - `/api/history` – returns historical metrics for a given hostname and date range
  - `/api/query` – runs custom SQL on the selected server (with security controls)
  - `/api/terminate` – sends terminate signal to a backend process (optional)

---

## Key Implementation Details

**Frontend:**
- Use React functional components and hooks (`useState`, `useEffect`)
- Main dashboard component manages connection state, server list, and tab state
- Real-time mode: connects to backend via Socket.IO, receives live updates
- Historical mode: only asks for hostname and date range, fetches from backend DB
- UI hides historical input panel until “Historical” is clicked
- All tables have CSV download buttons
- Responsive and modern UI (AppDynamics style)

**Backend:**
- Use `pg` npm package for PostgreSQL connections
- Use `socket.io` for real-time data push
- Poll all servers in credential file every 5 seconds, store results in central DB
- For `/api/history`, query the central DB for the requested hostname and time range
- Protect credential file and sensitive endpoints

**Credential File Example (JSON):**
```json
[
  {
    "name": "ProdDB",
    "host": "10.0.0.1",
    "port": 5432,
    "user": "readonly",
    "password": "secret",
    "database": "postgres",
    "unixUser": "osreadonly",
    "unixPassword": "ossecret"
  }
]
```

---

## Security & Offline Considerations

- All dependencies must be downloaded and installed offline (npm packages, etc.)
- No external API calls or CDN dependencies
- Store all code and assets locally
- Protect credential file and restrict access to backend endpoints

---

## Development Steps

1. **Set up backend:**
   - Node.js/Express app
   - Read credential file, poll all servers, store metrics in central DB
   - Implement REST and WebSocket endpoints

2. **Set up frontend:**
   - React app with Recharts
   - Implement dashboard UI, server selection, real-time and historical modes

3. **Test:**
   - Simulate multiple PostgreSQL servers (can use Docker locally)
   - Validate real-time and historical data flows

---

## Example File Structure

```
/server
  index.js
  poller.js
  credentials.json
  ...
/src
  App.jsx
  components/
    Dashboard.jsx
    CPUChart.jsx
    ReplicationLagChart.jsx
    ...
```

---

## Key UI Behaviors

- On load, fetch server list from backend
- User can select a server or enter details manually
- Real-time mode: live graphs and tables update every 5 seconds
- Historical mode: user enters hostname and date range, fetches from backend DB
- Historical panel is hidden until “Historical” is clicked

---

This writeup should allow your team to reproduce the same dashboard and backend in a restricted, offline environment using Copilot or manual development. All logic and UI/UX patterns are described for faithful recreation.
