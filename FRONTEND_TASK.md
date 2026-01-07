# Frontend Interview: Feature Flag Dashboard

## Context

You're building an internal admin dashboard for managing feature flags across our applications. A backend API is already running locally—your job is to build the frontend.

**Time:** ~30 minutes
**API:** `http://localhost:8080` (interactive docs at `/docs`)

---

## Requirements

### 1. Flag List View

Display all feature flags with the following information visible:

- Flag name and key
- Current enabled/disabled status (visually distinct)
- Environment (development, staging, production)
- Owner

The list should support:

- **Filtering by environment** — user can view flags for a specific environment or all environments
- **Search** — user can search by flag name or key

### 2. Toggle Functionality

Users must be able to toggle a flag's enabled status directly from the list view. The UI should:

- Reflect the updated state immediately
- Handle the API call appropriately

### 3. Create Flag Form

Provide a way for users to create a new feature flag. Required fields:

- Key (must be kebab-case, e.g., `my-new-flag`)
- Name
- Environment (select from: development, staging, production)

Optional fields:

- Description
- Owner

The form should:

- Validate the key format before submission
- Handle and display API errors (e.g., duplicate key)
- Clear or close after successful creation
- The new flag should appear in the list without a full page refresh

---

## Technical Expectations

- Use any framework you're comfortable with (React, Vue, Svelte, etc.)
- **Monorepo Structure**: You must set up a monorepo (e.g., using Turborepo, Nx, or workspaces) that contains both this existing backend and your new frontend application.
- Structure the project however you see fit within the monorepo
- Type safety is valued but not mandated
- Styling should be functional, not necessarily polished
- You have full access to AI tools, documentation, and the internet

---

## API Quick Reference

**Base URL:** `http://localhost:8080`

| Method | Endpoint                     | Description           |
| ------ | ---------------------------- | --------------------- |
| GET    | `/flags`                     | List all flags        |
| GET    | `/flags?environment=staging` | Filter by environment |
| GET    | `/flags?search=dark`         | Search by name/key    |
| POST   | `/flags`                     | Create a flag         |
| POST   | `/flags/:id/toggle`          | Toggle enabled status |

**Flag Shape:**

```typescript
interface FeatureFlag {
  id: string;
  key: string; // unique, kebab-case
  name: string;
  description: string | null;
  enabled: boolean;
  environment: "development" | "staging" | "production";
  metadata: {
    owner: string;
    tags: string[];
    expiresAt: string | null;
  };
  createdAt: string;
  updatedAt: string;
}
```

**Create Flag Request:**

```typescript
{
  key: string;          // required, kebab-case
  name: string;         // required
  environment: string;  // required
  description?: string;
  metadata?: {
    owner?: string;
  };
}
```

**Error Response:**

```typescript
{
  error: {
    code: string;
    message: string;
    details?: Array<{ field: string; message: string }>;
  }
}
```

---

## Not Required

The following are explicitly out of scope:

- Authentication/login
- Edit flag details (beyond toggle)
- Delete functionality
- Responsive/mobile design
- Automated tests
- Deployment configuration

---

## Evaluation Notes

We're observing:

- How you structure your project and components
- How you leverage AI tools in your workflow
- How you handle state and API integration
- How you approach the problem incrementally

There's no single "right" architecture. Make decisions you can explain.
