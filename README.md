# AI Workspace SaaS (Outpost)

A modern, full-stack collaborative workspace application powered by AI, designed to offer real-time document editing, task management, intelligent canvas interactions, and seamless cloud integrations.

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [Tech Stack](#-tech-stack)
- [Architecture & Technical Documentation](#-architecture--technical-documentation)
- [Documentation Links (Techdocs)](#-documentation-links-techdocs)
- [Installation & Local Development](#-installation--local-development)
- [Deployment](#-deployment)
- [License](#-license)
- [Connect & Acknowledgements](#-connect-with-me)

---

## 🎯 Project Overview

**AI Workspace SaaS** is an end-to-end, enterprise-grade collaborative platform designed to unite rich text editing, interactive diagramming, and artificial intelligence into a single user-friendly workspace. Built with modern web development practices, the application leverages real-time synchronization, modular micro-service patterns for messaging, securely isolated database tenancy, and custom export pipelines.

The platform provides users with an all-in-one hub where teams can organize notes, manage task workflows, auto-generate diagrams using embedded AI tools, and generate formatted PDF documents instantly.

---

## ✨ Key Features

- 📝 **Rich Block-Based Editing**: Powered by BlockNote for seamless, extensible, and modular document creation.
- 🤖 **Embedded AI Assistance**: Context-aware AI copilot for auto-summarization, content generation, and smart recommendations.
- 🎨 **Interactive Canvas & Diagramming**: Embedded design tools for brainstorming, architecture mapping, and flowcharting.
- 🔐 **Multi-Tenant Authentication & Access Control**: Secure user authentication and organization-based role management via Clerk.
- 💳 **Billing & Subscription Management**: Integrated billing pipelines using Stripe for SaaS tiered pricing models.
- 📄 **PDF & Document Export**: Native server/client-side document parsing and PDF exporting engine.
- ⚡ **Real-Time Collaboration**: Fast, reliable event messaging and state synchronization.

---

## 🛠️ Tech Stack

### Frontend & Framework

- **Framework**: [Next.js](https://nextjs.org/) (React 18 / App Router)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/), [Shadcn UI](https://ui.shadcn.com/)
- **Rich Text Editor**: [BlockNote](https://www.blocknotejs.org/)

### Backend & Database

- **Database**: PostgreSQL / [Supabase](https://supabase.com/) / [Prisma ORM](https://www.prisma.io/)
- **Messaging & Queueing**: Redis / Event-driven message brokers
- **Auth & User Management**: [Clerk](https://clerk.com/)

### Billing & Cloud Infrastructure

- **Payment Gateway**: [Stripe](https://stripe.com/)
- **Deployment**: Vercel / Cloudflare
- **Storage**: AWS S3 / Supabase Storage

---

## 📐 Architecture & Technical Documentation

The platform's architecture is structured to maintain high availability, strict data separation across tenants, and decoupled real-time messaging pipelines. Below is a detailed technical walkthrough based on the engineering specs located in the `/techdocs` directory.

### 1. High-Level Project Architecture

The overall platform architecture separates client presentation, API gateway logic, event streaming, and persistent storage layers into decoupled tiers.

<a href="./techdocs/Description_of_the_project_architecture.pdf" target="_blank">📄 Read Full Project Architecture Specification (PDF)</a>

![Outpost Project Overview](./techdocs/Outpost_project.jpg)
_Figure 1: High-level architectural layout showing data flow across user clients, edge services, API endpoints, database clusters, and external service integrations._

---

### 2. Messaging Architecture, Types & Components

The real-time messaging layer handles distributed events, real-time collaboration signals, notification triggers, and background job queuing.

<a href="./techdocs/Engineering_report%20.pdf" target="_blank">📄 Read Engineering Report (PDF)</a>

![Messaging Architecture - Types and Components](./techdocs/Messaging_architecture%20_-%20_types%20_and%20_components.jpg)
_Figure 2: Breakdown of event types, message queues, state management nodes, and component interactions within the real-time messaging system._

---

### 3. Edge Execution with Durable Objects & Cloudflare Workers

To handle stateful real-time interactions at low latency, the system routes state synchronization through Cloudflare Durable Objects and Workers.

![Durable Objects and Workers](./techdocs/Durable_objects_and_workers.jpg)
_Figure 3: Topology of stateful edge compute nodes utilizing Cloudflare Durable Objects for low-latency synchronization._

---

### 4. Server Actions vs. REST API Patterns

The application combines Next.js Server Actions for direct form and state updates with traditional REST API endpoints for external service integrations.

![Server Actions vs REST API](./techdocs/Server_actions_vs_REST_API.jpg)
_Figure 4: Comparative flow diagram contrasting Next.js Server Actions against traditional REST API endpoint execution._

---

### 5. Modal Window Management System

A centralized state management pattern handles global modal popups, confirmation dialogs, and workspace creation overlays.

![Modal Window Management](./techdocs/Modal_window_managment.jpg)
_Figure 5: State flow diagram of global modal context management across the client user interface._

---

## 📁 Documentation Links (Techdocs)

Access the raw documentation directory directly:
👉 **📁 [/techdocs Folder](./techdocs)**

### PDF Reports & Specifications

- <a href="./techdocs/Description_of_the_project_architecture.pdf" target="_blank">Description_of_the_project_architecture.pdf</a>
- <a href="./techdocs/Engineering_report%20.pdf" target="_blank">Engineering_report .pdf</a>

### Architectural Diagrams & Schematics

- [Durable_objects_and_workers.jpg](./techdocs/Durable_objects_and_workers.jpg)
- [Messaging*architecture *-\_types \_and \_components.jpg](./techdocs/Messaging_architecture%20_-%20_types%20_and%20_components.jpg)
- [Modal_window_managment.jpg](./techdocs/Modal_window_managment.jpg)
- [Outpost_project.jpg](./techdocs/Outpost_project.jpg)
- [Server_actions_vs_REST_API.jpg](./techdocs/Server_actions_vs_REST_API.jpg)

---

## 🚀 Installation & Local Development

### Prerequisites

- **Node.js**: `v18.x` or higher
- **Package Manager**: `npm`, `yarn`, or `pnpm`
- **PostgreSQL**: Local instance or remote connection string (e.g., Supabase)

### Step-by-Step Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/sxidsvit/ai-workspace-saas.git
   cd ai-workspace-saas
   ```

2. **Install dependencies:**

   ```bash
   npm install
   ```

3. **Configure Environment Variables:**
   Create a `.env.local` file in the root directory:

   ```env
   # App Config
   NEXT_PUBLIC_APP_URL=http://localhost:3000

   # Database / Prisma
   DATABASE_URL="postgresql://user:password@localhost:5432/ai_workspace?schema=public"

   # Clerk Authentication
   NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
   CLERK_SECRET_KEY=sk_test_...

   # Stripe Billing
   STRIPE_API_KEY=sk_test_...
   STRIPE_WEBHOOK_SECRET=whsec_...
   NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...

   # OpenAI / AI Services
   OPENAI_API_KEY=sk-...
   ```

4. **Initialize Database:**

   ```bash
   npx prisma db push
   ```

5. **Run Development Server:**

   ```bash
   npm run dev
   ```

6. Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## 🌐 Deployment

### Vercel Deployment

1. Import your GitHub repository into **Vercel**.
2. Add all environment variables listed in `.env.local`.
3. Deploy!

### Stripe Webhooks Setup

To process local or production subscription events, trigger webhooks using the Stripe CLI:

```bash
stripe listen --forward-to localhost:3000/api/webhooks/stripe
```

---

## 📜 License

This project is licensed under GPL-3.0-only.

The PDF export uses BlockNote's [`@blocknote/xl-pdf-exporter`](https://www.blocknotejs.org/docs/features/export/pdf), which is GPL-3.0 licensed, so the whole project is too. You can use, change and share this code, including commercially, as long as your version stays open source under GPL-3.0. To use it in a closed-source product, remove the PDF exporter or get a [BlockNote commercial license](https://www.blocknotejs.org/pricing).

---

### 📬 Connect with me

<a href="https://www.linkedin.com/in/sergiy-antonyuk/" target="_blank">
<img alt="Sergiy Antonyuk | LinkedIn" src="https://img.shields.io/badge/LinkedIn-0077B5.svg?&style=for-the-badge&logo=linkedin&logoColor=white" />
</a>

#### 🙏 Acknowledgements

This project is a version of the original project [Outpost](https://www.youtube.com/watch?v=vNXrFMSAsOA).

A heartfelt thank you to [Roadside Coder](https://www.youtube.com/@RoadsideCoder) for his invaluable contributions.

I used it for educational purposes to study its device in detail and created detailed technical documentation.
