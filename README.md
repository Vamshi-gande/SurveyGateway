# 📚 Monorepo Package Documentation

## 🟦 Backend Packages

**Located in:** `/apps/backend`

### Core

- **express** → Web framework to create APIs.
  ```javascript
  import express from "express";
  const app = express();
  ```

- **cors** → Enable Cross-Origin Resource Sharing.
  ```javascript
  import cors from "cors";
  app.use(cors());
  ```

- **helmet** → Secure Express with HTTP headers.
  ```javascript
  import helmet from "helmet";
  app.use(helmet());
  ```

- **dotenv** → Load .env variables.
  ```javascript
  import dotenv from "dotenv";
  dotenv.config();
  ```

### Database

- **@prisma/client** → Prisma ORM client.
  ```javascript
  import { PrismaClient } from "@prisma/client";
  const prisma = new PrismaClient();
  ```

- **prisma (dev)** → CLI for migrations, schema generation.
  ```bash
  npx prisma migrate dev
  ```

- **pg** → PostgreSQL driver (required by Prisma).

### Validation

- **zod** → Schema validation.
  ```javascript
  import { z } from "zod";
  const userSchema = z.object({ email: z.string().email() });
  ```

### Auth & RBAC

- **jsonwebtoken** → Issue & verify JWTs.
  ```javascript
  import jwt from "jsonwebtoken";
  const token = jwt.sign({ id: 1 }, process.env.JWT_SECRET!);
  ```

- **bcrypt** → Password hashing.
  ```javascript
  import bcrypt from "bcrypt";
  const hash = await bcrypt.hash("password", 10);
  ```

### File Handling / Ingestion

- **multer** → Handle file uploads.
  ```javascript
  import multer from "multer";
  const upload = multer({ dest: "uploads/" });
  app.post("/upload", upload.single("file"), (req, res) => { ... });
  ```

- **csv-parse** → Parse CSV files.
  ```javascript
  import { parse } from "csv-parse";
  ```

- **exceljs** → Create & manipulate Excel files (.xlsx) in Node.js or browser.
  ```javascript
  import ExcelJS from "exceljs";
  // Create workbook
  const workbook = new ExcelJS.Workbook();
  const sheet = workbook.addWorksheet("Report");
  // Add header
  sheet.addRow(["ID", "Name", "Age"]);
  // Add data rows
  sheet.addRow([1, "Alice", 25]);
  sheet.addRow([2, "Bob", 30]);
  // Save file
  await workbook.xlsx.writeFile("report.xlsx");
  ```

### Workers / Queues

- **bullmq** → Queue system.
  ```javascript
  import { Queue } from "bullmq";
  const ingestionQueue = new Queue("ingestion");
  ```

- **ioredis** → Redis client (used by BullMQ).
  ```javascript
  import Redis from "ioredis";
  const redis = new Redis(process.env.REDIS_URL);
  ```

### Utilities

- **uuid** → Generate unique IDs.
  ```javascript
  import { v4 as uuid } from "uuid";
  const id = uuid();
  ```

- **dayjs** → Date/time helper.
  ```javascript
  import dayjs from "dayjs";
  console.log(dayjs().format("YYYY-MM-DD"));
  ```

- **axios** → Call external APIs (future BharatKosh integration).
  ```javascript
  import axios from "axios";
  const res = await axios.get("https://api.example.com");
  ```

### Dev / Tooling

- **typescript** → TypeScript compiler.
- **ts-node / ts-node-dev** → Run TS files in dev mode.
- **eslint / prettier** → Linting & formatting.
- **@types/** → TypeScript definitions.

## 🟩 Frontend Packages

**Located in:** `/apps/frontend`

### Core

- **react + react-dom** → UI library.

- **react-router-dom** → Routing.
  ```javascript
  import { BrowserRouter, Route } from "react-router-dom";
  ```

- **axios** → API client.

### State & Data Fetching

- **@tanstack/react-query** → Data fetching, caching.
  ```javascript
  const { data } = useQuery(["datasets"], fetchDatasets);
  ```

- **zustand** → Lightweight state management.
  ```javascript
  import create from "zustand";
  const useStore = create(set => ({ 
    role: "PUBLIC", 
    setRole: r => set({ role: r }) 
  }));
  ```

### UI / Styling

- **bootstrap** → CSS framework.
  ```javascript
  import 'bootstrap/dist/css/bootstrap.min.css';
  ```

- **react-bootstrap** → React components for Bootstrap.
  ```javascript
  import { Button } from 'react-bootstrap';
  <Button variant="primary">Click</Button>
  ```

- **lucide-react** → Icon library.
  ```javascript
  import { Home } from 'lucide-react';
  <Home />
  ```

- **shadcn/ui** → UI components.

### Forms & Validation

- **react-hook-form** → Forms.
  ```javascript
  const { register, handleSubmit } = useForm();
  ```

- **@hookform/resolvers** → Integrates with Zod.
- **zod** → Shared validation schemas.

### Tables & Charts

- **@tanstack/react-table** → Advanced tables.
- **recharts** → Charts.

### Utilities

- **dayjs / uuid** → Date & ID utilities.

### Dev

- **vite** → Build tool.
- **@vitejs/plugin-react** → React support.
- **eslint / prettier** → Linting/formatting.
- **@types/** → Type definitions.

## 🟨 Shared Packages

**Located in:** `/shared`

- **zod** → Shared validation schemas.
  ```javascript
  export const datasetSchema = z.object({ 
    id: z.number(), 
    title: z.string() 
  });
  ```

- **typescript** → For type definitions.
- **tslib** → Helper library for TS.
- **eslint / prettier** → Formatting.

## 🟥 Root Packages

**Located in:** `/project-root`

- **concurrently** → Run backend + frontend in parallel.
  ```bash
  npm run dev:all
  ```

- **eslint / prettier** → Lint & format at root.
- **typescript** → Global TS config.

## ⚡ Installation

From the root workspace:

```bash
# Install all backend + frontend + shared deps in one go
npm install
```

This installs everything because root package.json has:

```json
"workspaces": [
  "apps/*",
  "shared"
]
```