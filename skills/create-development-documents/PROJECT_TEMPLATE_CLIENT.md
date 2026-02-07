# Client Project Specification Template

> **Instructions**: Fill in the essential information below. The skill will gather additional details from your codebase as needed.

---

## 1. Project Basics

- **Project Name**: [Your project name]
- **Project Type**: [e.g., Web App, Mobile App, SPA, Dashboard, PWA]
- **Description**: [1-2 sentence description]
- **Core Problem Solved**: [What problem does this solve?]

---

## 2. Technology Stack

### Frontend

- **Framework**: [e.g., React Router v7, Next.js, Vue, Angular, React Native]
- **Language**: [e.g., TypeScript, JavaScript]
- **State Management**: [e.g., React Context, Redux, Zustand, TanStack Query, None]
- **Styling**: [e.g., Tailwind CSS, CSS Modules, SCSS, Styled Components]
- **Build Tool**: [e.g., Vite, Webpack, Turbopack]
- **UI Library**: [e.g., shadcn/ui, Material UI, Ant Design, None]

### Testing & Tools

- **Unit/Integration Test**: [e.g., Vitest, Jest, Testing Library]
- **E2E Framework**: [e.g., Playwright, Cypress, None]
- **Package Manager**: [e.g., npm, pnpm, yarn]
- **Code Quality**: [e.g., ESLint, Prettier, TypeScript strict mode]

---

## 3. Key Features (3-5 main features)

1. [Feature 1 - e.g., User authentication UI]
2. [Feature 2 - e.g., Product browsing and search interface]
3. [Feature 3 - e.g., Shopping cart and checkout flow]
4. [Feature 4 - e.g., User profile management]
5. [Feature 5 - e.g., Responsive dashboard]

---

## 4. Core User Flows (Top 2-3)

**Flow 1: [e.g., User Registration]**

1. [Step 1 - e.g., User clicks "Sign Up" button]
2. [Step 2 - e.g., User fills in registration form]
3. [Step 3 - e.g., System validates and creates account, redirects to dashboard]

**Flow 2: [e.g., Product Purchase Flow]**

1. [Step 1 - e.g., User browses product catalog]
2. [Step 2 - e.g., User adds items to cart and proceeds to checkout]
3. [Step 3 - e.g., User completes payment and receives confirmation]

---

## 5. Main Routes (Top 5-10)

| Path             | Description         | Auth? | Key Components            |
| ---------------- | ------------------- | ----- | ------------------------- |
| `/`              | Home page           | No    | Hero, ProductList         |
| `/login`         | Login page          | No    | LoginForm                 |
| `/signup`        | Registration page   | No    | SignupForm                |
| `/dashboard`     | User dashboard      | Yes   | DashboardLayout, Stats    |
| `/products`      | Product listing     | No    | ProductGrid, Filters      |
| `/products/:id`  | Product detail      | No    | ProductDetail             |
| `/cart`          | Shopping cart       | Yes   | CartItems, CheckoutButton |
| `/checkout`      | Checkout flow       | Yes   | PaymentForm               |
| `/profile`       | User profile        | Yes   | ProfileForm               |

---

## 6. UI Components (Key reusable components)

1. **[Component 1 - e.g., Button]**: Primary, secondary, disabled states
2. **[Component 2 - e.g., ProductCard]**: Display product info with image, price, CTA
3. **[Component 3 - e.g., Navigation]**: Main navigation with auth state
4. **[Component 4 - e.g., Modal]**: Reusable modal for various dialogs
5. **[Component 5 - e.g., Form]**: Form wrapper with validation

---

## 7. Domain Terminology (3-5 key terms)

1. **[Term 1 - e.g., User]**: [Person who browses and purchases products]
2. **[Term 2 - e.g., Cart]**: [Temporary collection of selected products]
3. **[Term 3 - e.g., Wishlist]**: [Saved products for future purchase]

---

## 8. Environment Setup

**Prerequisites**: [e.g., Node.js 20+]

### Frontend Setup

```bash
# [Install command - e.g., npm install]
# [Start command - e.g., npm run dev]
# [Build command - e.g., npm run build]
# [Test command - e.g., npm run test]
```

**Environment Variables**:

```env
# API
VITE_API_URL=
VITE_API_KEY=
# Auth
VITE_AUTH_DOMAIN=
# External Services
VITE_ANALYTICS_ID=
```

---

## 9. Testing Strategy

- **Unit Test Coverage**: [e.g., 70% for components and utilities]
- **Integration Tests**: [e.g., Key user flows]
- **E2E Tests**: [e.g., Critical paths only]
- **Visual Regression**: [e.g., Storybook, Chromatic, None]
- **Testing Philosophy**: [e.g., TDD, Test-after, None]

---

## 10. UI/UX Configuration

### Design System

- **Color Palette**: [e.g., Primary, Secondary, Accent colors]
- **Typography**: [e.g., Font families, sizes, weights]
- **Spacing System**: [e.g., 4px base, 8px increments]
- **Breakpoints**: [e.g., sm: 640px, md: 768px, lg: 1024px, xl: 1280px]
- **Design Tokens**: [e.g., CSS variables, Tailwind config, Theme object]

### Accessibility

- **ARIA Support**: [e.g., Required for interactive components]
- **Keyboard Navigation**: [e.g., Full keyboard support]
- **Screen Reader**: [e.g., Tested with NVDA/VoiceOver]
- **WCAG Level**: [e.g., AA compliance, None]

### Performance

- **Code Splitting**: [e.g., Route-based, Component-based]
- **Lazy Loading**: [e.g., Images, routes, heavy components]
- **Caching Strategy**: [e.g., Service worker, Cache-first for assets]
- **Bundle Size Target**: [e.g., < 200kb initial bundle]

### State Management

- **Local State**: [e.g., useState, useReducer]
- **Global State**: [e.g., Context, Redux, Zustand]
- **Server State**: [e.g., TanStack Query, SWR, RTK Query]
- **Form State**: [e.g., React Hook Form, Formik, Native]

---

## 11. Architecture Notes

**Why this stack?**
[Brief explanation of why you chose these technologies]

**Key Constraints**:
[Any important technical or business constraints]

**Component Structure**: [e.g., Atomic Design, Feature-based, Domain-driven]

**Routing Strategy**: [e.g., File-based, Config-based, Dynamic]

---

## 12. Optional: Additional Information

### Third-Party Services (if used)

- **Auth**: [e.g., Clerk, Auth0, Supabase Auth, None]
- **Analytics**: [e.g., Google Analytics, Mixpanel, Plausible, None]
- **Error Tracking**: [e.g., Sentry, LogRocket, None]
- **CDN**: [e.g., CloudFlare, CloudFront, None]
- **Maps**: [e.g., Google Maps, Mapbox, None]
- **Payments**: [e.g., Stripe Elements, PayPal SDK, None]

### Non-Functional Requirements

- **Performance**: [e.g., Page load < 2s, First Contentful Paint < 1s]
- **Browser Support**: [e.g., Last 2 versions of major browsers]
- **Mobile Support**: [e.g., iOS 14+, Android 10+]
- **Offline Support**: [e.g., Service worker, Cache API, None]
- **SEO**: [e.g., SSR/SSG for public pages, Meta tags, Sitemap]

### Deployment

- **Hosting**: [e.g., Vercel, Netlify, AWS S3 + CloudFront]
- **CI/CD**: [e.g., GitHub Actions, Vercel auto-deploy]
- **Preview Environments**: [e.g., Per PR, Per branch, None]
- **Environment Stages**: [e.g., Dev, Staging, Production]

---

**That's it!** The skill will use this information plus your codebase to generate comprehensive documentation.
