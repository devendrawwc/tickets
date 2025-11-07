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
