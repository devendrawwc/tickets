# tickets
AI First - Book Tickets, accept payments, share receipts, run loyalty program, ad support. Browser, Mobile. Astro, Solid, Tailwindcss, Typescript, Bun, PostgreSQL

ASTRO + SOLID CONSTRAINTS:
✓ Static by default, client:visible for interactivity
✓ createSignal/createEffect (NO useState/useEffect)
✓ on:click (NO onClick)
✓ class (NO className)
✓ signal() with parentheses to read value
✓ nanostores with $ prefix (NO Context)
✓ Tailwind only (NO inline styles)
✓ @/ imports (NO ../..)
✓ File-based routing (NO client router)
✓ Progressive forms (work without JS)

# ConstructAid.ai Development Guidelines

## Stack
- Astro 4.x (Static site generator + islands)
- Solid.js (Reactive UI library)
- TailwindCSS (Utility-first styling)
- TypeScript + Zod (Type safety + runtime validation)
- nanostores (Global state)

## Core Principles

### 1. Astro Islands Architecture
- Components are **static HTML by default**
- Add `client:` directive ONLY when interactivity needed:
  - `client:load` - Critical interactive elements (rare)
  - `client:visible` - Below-fold interactive content (common)
  - `client:idle` - Non-critical enhancements (common)
- Server code in `---` frontmatter runs at **BUILD time**
- For request-time logic, use API routes or Astro actions

### 2. Solid.js Patterns (NOT React)
- State: `createSignal()` - signals are functions: `count()` not `count`
- Effects: `createEffect()` - auto-tracks, no dependency array
- Memoization: `createMemo()` for derived values
- Events: `on:click` not `onClick` (lowercase with colon)
- No hooks rules, no stale closures, just signals

### 3. State Management
- **Local state**: `createSignal()` within component
- **Global state**: nanostores with `$` prefix
```ts
  import { atom } from 'nanostores';
  export const $bills = atom([]);
```
- **Never**: React Context, Redux, Zustand

### 4. Styling Rules
- **Only** Tailwind utility classes
- Use `class` not `className`
- No inline styles, no CSS-in-JS, no styled-components
- Component composition over style props

### 5. Type Safety
- Define Zod schemas first
- Infer TypeScript types: `type Bill = z.infer<typeof BillSchema>`
- All API inputs/outputs validated with Zod
- No `any` types

### 6. File Structure
```
src/
├── components/
│   ├── ui/          # Generic reusable
│   └── bills/       # Feature-specific
├── pages/           # Astro routes
├── lib/             # Business logic
├── types/           # Type definitions
└── stores/          # nanostores
```

### 7. Import Paths
- Always use `@/` alias
- Never more than one `../` 
- Example: `import { BillSchema } from '@/types/bills'`

### 8. Forms
- Work without JavaScript (progressive enhancement)
- Use Astro actions for server-side handling
- Client-side validation as enhancement only

### 9. Data Fetching
- **Build-time**: Fetch in `---` frontmatter
- **Request-time**: Astro actions or API routes
- **Client-side**: Only for truly dynamic data (rare)

### 10. No Client-Side Routing
- Use Astro's file-based routing in `src/pages/`
- Standard `<a href>` for navigation
- No `@solidjs/router` or similar

## Common Mistakes to Avoid

❌ `useState`, `useEffect` → ✅ `createSignal`, `createEffect`
❌ `onClick` → ✅ `on:click`
❌ `className` → ✅ `class`
❌ `count` → ✅ `count()`
❌ Context API → ✅ nanostores
❌ `client:load` everywhere → ✅ Static by default
❌ CSS-in-JS → ✅ Tailwind only
❌ Relative imports → ✅ `@/` alias

## Example Component
```tsx
// BillCard.tsx
import { Component } from 'solid-js';
import { BillSchema } from '@/types/bills';
import type { z } from 'zod';

type Bill = z.infer<typeof BillSchema>;

export const BillCard: Component<{ bill: Bill }> = (props) => {
  const [expanded, setExpanded] = createSignal(false);
  
  return (
    <div class="rounded-lg border p-4">
      <h3 class="text-lg font-semibold">{props.bill.title}</h3>
      <button 
        on:click={() => setExpanded(!expanded())}
        class="text-blue-600 hover:text-blue-800"
      >
        {expanded() ? 'Collapse' : 'Expand'}
      </button>
    </div>
  );
};
```

Always follow these patterns. Ask for clarification if unclear.
```

---

## How to Use This

### **Option 1: Cursor .cursorrules file**
Create `.cursorrules` in project root (Cursor reads this automatically):
```
[paste the master prompt template above]
```

### **Option 2: Claude Projects Instructions**
In Claude.ai Projects, add the markdown as project instructions.

### **Option 3: Inline Prompts**
For one-off prompts, add:
```
Follow Astro + Solid patterns:
- Astro Islands (client: only when needed)
- Solid signals (createSignal, on:click)
- nanostores for global state
- Tailwind only, no CSS-in-JS
- @/ imports
[paste your specific request]
```

---

## Quick Reference Card

**Keep this handy for prompts:**
```
ASTRO + SOLID CONSTRAINTS:
✓ Static by default, client:visible for interactivity
✓ createSignal/createEffect (NO useState/useEffect)
✓ on:click (NO onClick)
✓ class (NO className)
✓ signal() with parentheses to read value
✓ nanostores with $ prefix (NO Context)
✓ Tailwind only (NO inline styles)
✓ @/ imports (NO ../..)
✓ File-based routing (NO client router)
✓ Progressive forms (work without JS)
