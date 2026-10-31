# Current functionality

This repository is the starting scaffold for Tetris IDE. It currently includes the Next.js App Router, React, TypeScript, Tailwind CSS, shadcn/ui components, Inter/IBM Plex Mono fonts, and Clerk authentication provider/middleware setup. The product-specific Tetris and IDE features have not been implemented yet.

## Setup progress

- [x] Add shadcn/ui components with `bunx shadcn@latest add --all`. Components are in `src/components/ui/`.
- [x] Install `next-themes`.
- [x] Add the theme provider and wrap the app in it from `src/app/layout.tsx`.
- [x] Update `src/app/globals.css` with customized shadcn theme variables, light/dark colors, radius tokens, and animation styles.
- [x] Configure the Tailwind dark variant and base styles in `src/app/globals.css`.
- [x] Add custom CSS for button cursors, the cell-ripple animation, and scrollbars in `src/app/additional.css`.
- [x] Install `@clerk/nextjs` and wrap the app with `ClerkProvider` in `src/app/layout.tsx`.
- [x] Add Clerk middleware using `clerkMiddleware` in `src/proxy.ts`.
- [ ] Add sign-in/sign-up UI and user account controls.

To repeat the component-generation step:

```bash
bunx shadcn@latest add --all
```

### Implement dark mode

1. Install `next-themes`:

   ```bash
   bun add next-themes
   ```

2. Create `src/components/theme-provider.tsx`:

   ```tsx
   "use client"

   import * as React from "react"
   import { ThemeProvider as NextThemesProvider } from "next-themes"

   export function ThemeProvider({
      children,
      ...props
   }: React.ComponentProps<typeof NextThemesProvider>) {
      return <NextThemesProvider {...props}>{children}</NextThemesProvider>
   }
   ```

3. Import the provider in `src/app/layout.tsx` and wrap the page content:

   ```tsx
   import { ThemeProvider } from "@/components/theme-provider"

   // Inside the root layout:
   ;<body>
      <ThemeProvider>{children}</ThemeProvider>
   </body>
   ```

4. Configure the light/dark theme variables and Tailwind dark variant in `src/app/globals.css`.

### Set up Clerk authentication

1. Install Clerk for Next.js:

   ```bash
   bun add @clerk/nextjs
   ```

2. Wrap the root layout with `ClerkProvider` from `@clerk/nextjs`.
3. Add `src/proxy.ts` with `clerkMiddleware()` and configure its matcher for app pages and API routes.
4. Add Clerk environment keys and implement sign-in/sign-up and account UI before using authentication in the app.
