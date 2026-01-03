# Fullstack Next.js Template Documentation

This project is a Fullstack boilerplate using **Next.js (App Router)**, **TypeScript**, and **Tailwind CSS**. The project structure is designed to be scalable, modular, and maintainable with a clear separation of concerns between UI, Logic, and API.

## 📂 Directory Structure

Here is an overview of the project directory structure:

```
/
├── .vscode/               # VS Code configuration
├── public/                # Static assets (images, svgs)
├── src/
│   ├── @types/            # Global TypeScript type definitions
│   ├── app/               # Next.js App Router (Entry points for Pages & API)
│   │   ├── api/           # API Routes (Server-side entry points)
│   │   ├── layout.tsx     # Root layout
│   │   └── page.ts        # Root page redirection/render
│   ├── configs/           # Global configurations (Environment, Constants)
│   ├── designs/           # Global styling & CSS utilities (Tailwind)
│   ├── modules/           # Feature/Domain modules (Logic & UI specific to features)
│   │   └── {ModuleName}/
│   │       ├── services/  # Business logic (Controller, Model, Routes)
│   │       └── {Page}.tsx # Page UI Components
│   └── packages/          # Shared libraries & utilities (Reusables)
│       ├── hooks/         # Custom React Hooks
│       ├── libs/          # Library wrappers (e.g., BaseHttp)
│       ├── server/        # Server-side utilities (BaseController, Middlewares)
│       └── utils/         # General helper functions
├── eslint.config.mjs      # ESLint Flat Config
├── next.config.ts         # Next.js Configuration
├── postcss.config.mjs     # PostCSS Configuration (for Tailwind)
└── tsconfig.json          # TypeScript Configuration
```

---

## 🏗️ Architecture & Design Patterns

### 1. Modular Architecture (`src/modules`)
Each main feature is grouped into its own module under `src/modules`. This keeps related code close together.
- **UI Components**: Page components or feature-specific UI parts.
- **Services**: Backend business logic, controllers, and data models.

### 2. Server-Side Pattern (`src/packages/server`)
For API Routes, this project uses a lightweight **Controller-Model** pattern:
- **BaseController**: `src/packages/server/base/Controller.ts` provides standard helper methods like `sendJSON`, `handleError`, and `setError`.
- **Controller**: Extends `BaseController`. Methods are defined as arrow functions to preserve `this` context.
- **Model**: Simple objects or classes handling data fetching or database logic.
- **Route Handler**: In `src/app/api/.../route.ts`, we simply export the method from the Controller.

**API Flow Example:**
`src/app/api/quotes/random/route.ts` -> `QuoteController.random` -> `QuoteModel.random`

### 3. Client-Side HTTP Client (`src/packages/libs/BaseHttp`)
A native `fetch` wrapper that provides standard error handling and typing.
- Location: `src/packages/libs/BaseHttp/index.ts`
- Usage: `Http.get(...)`, `Http.post(...)`
- Automatically handles JSON parsing and error throwing.

### 4. Path Aliases
The project uses path aliases for cleaner imports:
- `@/*` -> `./src/*`
- `#/*` -> `./public/*`

---

## 📏 ESLint & Coding Conventions

This project uses **ESLint Flat Config** (`eslint.config.mjs`) with strict rules to maintain code consistency.

### Key Rules
- **Indentation**: 2 spaces.
- **Quotes**: Single quotes (`'`) preferred, except for template literals.
- **Semicolons**: Mandatory (`always`).
- **Trailing Commas**: Disallowed (`never`).
- **Spacing**:
  - Space after comma, not before.
  - Space inside object curly braces `{ key: value }`.
  - No space inside parentheses `(arg)`.
- **React**:
  - JSX uses double quotes.
  - Multiline JSX wrapped in parentheses `()`.
  - `react-hooks/exhaustive-deps` enabled (warn).
- **Console**: `console.log` disallowed in production (warn).

### Naming Conventions
- **Variables/Functions**: `camelCase`
- **Constants**: `CAPITALIZED_SNAKE_CASE`
- **Components**: `PascalCase`
- **Files**:
  - Component/Page: `PascalCase.tsx` (e.g., `Home.page.tsx`)
  - Utilities/Functions: `camelCase.ts`
  - Classes/Models: `PascalCase.ts`

### Main Dependencies
- **Framework**: Next.js 15 (App Router)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS 4
- **Linter**: ESLint 9

---

## 🚀 How to Use This Boilerplate

1. **Create a New Module**:
   Create a folder in `src/modules/FeatureName`.
2. **Create UI**:
   Add React components inside that module.
3. **Create API (Optional)**:
   - Create a `Model` in `src/modules/FeatureName/services`.
   - Create a `Controller` that extends `BaseController`.
   - Create a route in `src/app/api/feature-name/route.ts` and connect it to the Controller.
4. **Styling**:
   Use Tailwind classes. Global utilities are in `src/designs`.
