# One Sports

## **Project Structure**

```plaintext
one-sports/
├── public/                  # Static assets (logos, images, etc.)
├── src/
│   ├── app/
│   │   ├── layout.tsx       # Root layout (Header, Footer)
│   │   ├── page.tsx         # Home page (Latest sports articles)
│   │   ├── [category]/      # Dynamic route for sports categories (e.g., Football, Basketball)
│   │   │   ├── page.tsx     # Category page
│   │   │   ├── layout.tsx   # Optional category-specific layout
│   │   ├── article/         # Dynamic route for individual articles
│   │   │   ├── [id]/        # Article details page
│   │   │   │   ├── page.tsx # Article details
│   ├── components/          # Reusable components (Header, Footer, ArticleCard, etc.)
│   │   ├── Header.tsx
│   │   ├── Footer.tsx
│   │   ├── ArticleCard.tsx
│   │   └── LoadingSpinner.tsx
│   ├── services/            # API interaction logic
│   │   ├── apiClient.ts     # Axios or Fetch setup
│   │   └── sportsService.ts # Functions for fetching articles, categories, etc.
│   ├── styles/              # (Optional) CSS/SCSS or Tailwind configuration
│   │   ├── globals.css      # Global styles
│   │   └── variables.css    # CSS variables or theming
│   ├── utils/               # Utility/helper functions
│   │   ├── formatDate.ts    # Example: Format dates for articles
├── package.json
├── tsconfig.json
├── next.config.js
└── README.md
```

---

## **Folder Breakdown**

### `app/`
This is the primary directory for routing and UI rendering using the Next.js App Router.

### `components/`
Holds reusable components like `Header`, `Footer`, and `ArticleCard`.

#### Files and Folders:
- **`layout.tsx`**: The root layout file that defines the base structure for all pages.
- **`page.tsx`**: The homepage, which fetches and displays the latest sports articles.
- **`[category]/page.tsx`**: Dynamic category pages (e.g., `/football` or `/basketball`) to fetch and display articles from specific categories.
- **`article/[id]/page.tsx`**: Dynamic article pages that fetch and display full details of a specific article

### `services/`
Handles interaction with third-party APIs. This is where functions to fetch articles, categories, and other data are implemented.

### `styles/`
Contains global and reusable styles for the app. (Optional)

### `utils/`
Holds helper functions like formatting dates.

---

## **Code Samples**

### `app/layout.tsx`
Defines the root layout, including shared UI elements.

```tsx
import { ReactNode } from "react"

// components
import Header from '@/components/Header'
import Footer from '@/components/Footer'

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <Header />
        <main>{children}</main>
        <Footer />
      </body>
    </html>
  )
}
```

### `app/page.tsx`
Homepage that fetches and displays the latest sports articles.

```tsx
// service
import apiClient from '@/services/apiClient'

// component
import ArticleCard from '@/components/ArticleCard'

export default async function HomePage() {
  const articles = await apiClient.get('/sports/latest')

  return (
    <div>
      <h1>Latest Sports News</h1>
      <div>
        {articles.map((article: any) => (
          <ArticleCard key={article.id} article={article} />
        ))}
      </div>
    </div>
  )
}
```
---