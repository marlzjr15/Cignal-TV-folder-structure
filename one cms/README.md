
# One CMS

## Project Structure

```
/one-cms
├── /public                    # Static assets (logos, images, etc.)
├── /src                       
│   ├── /app                   
│   │   ├── /auth/             # Authentication routes
│   │   │   ├── layout.tsx     # Layout for authentication pages
│   │   │   ├── page.tsx       # Login page
│   │   │   └── otp/           # OTP verification page
│   │   │   │   └── page.tsx
│   │   ├── /dashboard/        # Dashboard routes
│   │   │   ├── layout.tsx     # Layout for dashboard pages
│   │   │   ├── page.tsx       # Dashboard index page
│   │   │   └── cms/           # CMS content rendering page
│   │   │   │   └── page.tsx
│   │   ├── /api/              # API routes (using Next.js Edge or serverless functions)
│   │   │   ├── login/         # API route for user login
│   │   │   │   └── route.ts
│   │   │   ├── verify-2fa/    # API route for verifying 2FA code
│   │   │   │   └── route.ts
│   │   ├── page.tsx           # Home page (replaces /index.tsx)
│   │   ├── layout.tsx         # Root layout for the entire application
│   │   └── error.tsx          # Global error boundary for the app
│   ├── /components            # Reusable components
│   │   ├── LoginForm.tsx      # Login form component
│   │   ├── OTPForm.tsx        # OTP form component
│   │   ├── CMSContent.tsx     # Component for rendering Webiny CMS content
│   │   └── LoadingSpinner.tsx # Loading spinner for suspense
│   ├── /graphql               # GraphQL-related logic
│   │   ├── client.ts          # GraphQL client setup
│   │   ├── queries/           # GraphQL queries
│   │   │   └── getPosts.ts    # Example query for fetching posts
│   │   └── mutations/         # GraphQL mutations
│   ├── /services              # Service helpers
│   │   ├── auth.ts            # Helper functions for authentication
│   │   ├── 2fa.ts             # Helper functions for 2FA
│   │   └── webiny.ts          # Functions to fetch data from Webiny GraphQL API
│   ├── /styles                # (Optional) CSS/SCSS or Tailwind configuration
│   │   └── globals.css        # Global styles
│   │   └── variables.css      # CSS variables or theming
│   ├── /utils                 # Utility functions
│   │   ├── formatDate.ts      # Format dates
│   │   ├── formatSlug.ts      # Format slugs
├── /package.json              
├── /tsconfig.json             
├── /next.config.js            
└── /README.md                 
```

---

## **Folder Breakdown**

### `app/`
This is the primary directory for routing and UI rendering using the Next.js App Router.

#### Files and Folders:
- **`auth/`**: Contains authentication-related pages (e.g., Login and OTP verification).
- **`dashboard/`**: Contains dashboard-related pages and CMS content 
- **`api/`**: Defines serverless API routes like login and verify-2fa.
- **`layout.tsx`**: The root layout file that defines the base structure for all pages.
- **`page.tsx`**: The homepage of the app.
- **`error.tsx`**: Global error boundary to handle unexpected errors in the app.

### `components/`
Holds reusable UI components like `LoginForm`, `CMSContent`, `OTPForm`, and `LoadingSpinners`.

### `graphql/`
Contains helper functions for external service interactions, such as:

- **`auth.ts`**: Authentication logic (e.g., JWT handling).
- **`2fa.ts`**: Logic for generating and verifying 2FA codes.
- **`webiny.ts`**: Functions to fetch data from the Webiny CMS API.

### `styles/`
Contains global and reusable styles for the app. (Optional)

### `utils/`
Utility functions to support the application, like:

- **`formatDate.ts`**: Formats dates for display.
- **`formatSlug.ts`**: Formats strings to URL-friendly slugs.

---

## **Code Samples**

### `app/layout.tsx`
Defines the root layout, including shared UI elements.

```tsx
import { ReactNode } from 'react'

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <main>{children}</main>
      </body>
    </html>
  )
}
```

### `app/auth/layout.tsx`
A layout specific to authentication pages.

```tsx
import { ReactNode } from 'react'

export default function AuthLayout({ children }: { children: React.ReactNode }) {
  return (
    <div>
      {children}
    </div>
  );
}
```

### `app/auth/page.tsx`
Login page for user authentication:

```tsx
import LoginForm from '@/components/LoginForm'

export default function LoginPage() {
  return (
    <div>
      <h1>Login</h1>
      <LoginForm />
    </div>
  );
}
```

### `app/api/login/route.ts`
Handles user login on the server.

```tsx
import { NextResponse } from 'next/server'

export async function POST(req: Request) {
  try {
    const { email, password } = await req.json()

    // Add authentication logic here
    if (email === 'test@example.com' && password === 'password123') {
      return NextResponse.json(
        { success: true, message: 'Login successful!' },
        { status: 200 }
      )
    }

    return NextResponse.json(
      { success: false, message: 'Invalid credentials.' },
      { status: 401 }
    )
  } catch (error) {
    return NextResponse.json(
      { success: false, message: error.message },
      { status: 500 }
    )
  }
}
```
---