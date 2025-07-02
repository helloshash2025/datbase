# Initial Requirements for PostgreSQL Monitoring Dashboard

To set up and run the full dashboard (frontend and backend) in an offline or restricted environment, you will need the following prerequisites and dependencies. This checklist ensures you can build, run, and develop the project without internet access.

---

## 1. System Requirements
- **Node.js** (v18.x or later recommended)
- **npm** (comes with Node.js)
- **PostgreSQL** (for storing historical metrics and as the monitored target)
- **Git** (for version control, optional but recommended)

## 2. Node.js Dependencies (Frontend & Backend)
You must have all npm packages available locally. These are the main dependencies (see `package.json` for exact versions):

### Backend (Node.js/Express)
- express
- socket.io
- pg
- cors
- dotenv
- (optional) node-cron, ssh2, winston, etc.

### Frontend (React)
- react
- react-dom
- recharts
- socket.io-client
- axios
- (optional) react-scripts, vite, etc.

## 3. Local Installation Steps
1. **Clone or copy the project folder** to your target machine.
2. **Install Node.js** and npm if not already present.
3. **Install all dependencies locally:**
   - If you have internet access once, run:
     ```sh
     npm install
     cd server && npm install
     ```
   - If you are fully offline, copy the `node_modules` and `package-lock.json` from a prepared machine, or use a local npm registry (e.g., Verdaccio).
4. **Set up your PostgreSQL database** for storing metrics.
5. **Create and configure your credential file** (e.g., `credentials.json`).
6. **Configure environment variables** (see `.env.example` or README).

## 4. Optional Tools
- **PM2** (for running Node.js apps as services)
- **Docker** (for containerized deployment, if allowed)

## 5. Example Directory Structure
```
/project-root
  /server
    index.js
    ...
  /src
    App.jsx
    ...
  package.json
  package-lock.json
  .env
  credentials.json
```

## 6. How to Start
- **Backend:**
  ```sh
  cd server
  node index.js
  ```
- **Frontend:**
  ```sh
  npm run dev
  # or
  npm start
  ```

---

## 7. Summary Checklist
- [ ] Node.js and npm installed
- [ ] All npm dependencies available locally
- [ ] PostgreSQL running and accessible
- [ ] Credentials file created
- [ ] Environment variables configured
- [ ] node_modules present (or local npm registry set up)

---

This file can be used as a one-stop checklist for your IT or DevOps team to prepare the environment for the dashboard, even in a fully offline or restricted network.
