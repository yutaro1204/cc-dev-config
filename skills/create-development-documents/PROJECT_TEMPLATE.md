# Project Specification Template

> **Instructions**: Fill in the essential information below. The skill will gather additional details from your codebase as needed.

---

## 1. Project Basics

- **Project Name**: [Your project name]
- **Project Type**: [e.g., E-commerce, SaaS, API, Dashboard, Mobile app]
- **Description**: [1-2 sentence description]
- **Core Problem Solved**: [What problem does this solve?]

---

## 2. Technology Stack

### Core Technologies

- **Frontend Framework**: [e.g., React Router v7, Next.js, Vue, Angular, None]
- **Backend Framework**: [e.g., Express, Django, FastAPI, Rails, Same as frontend]
- **Language**: [e.g., TypeScript, Python, Java, Go]
- **Database**: [e.g., PostgreSQL, MongoDB, MySQL]
- **ORM**: [e.g., Prisma, TypeORM, SQLAlchemy, Mongoose]

### Infrastructure

- **Cache**: [e.g., Redis, Valkey, None]
- **Storage**: [e.g., S3, Local, Cloud Storage, None]
- **Container**: [e.g., Docker Compose, None]
- **Cloud/Hosting**: [e.g., AWS, Vercel, Self-hosted]

### Testing & Tools

- **Test Framework**: [e.g., Vitest, Jest, Pytest]
- **E2E Framework**: [e.g., Playwright, Cypress, None]
- **Styling**: [e.g., Tailwind CSS, CSS Modules, SCSS]
- **Package Manager**: [e.g., npm, pnpm, pip, yarn]

---

## 3. Key Features (3-5 main features)

1. [Feature 1 - e.g., User authentication and authorization]
2. [Feature 2 - e.g., Product catalog with search]
3. [Feature 3 - e.g., Shopping cart and checkout]
4. [Feature 4 - e.g., Admin dashboard]
5. [Feature 5 - e.g., Order management]

---

## 4. Core User Flows (Top 2-3)

**Flow 1: [e.g., User Registration]**

1. [Step 1]
2. [Step 2]
3. [Step 3]

**Flow 2: [e.g., Purchase Flow]**

1. [Step 1]
2. [Step 2]
3. [Step 3]

---

## 5. Data Models (Top 3-5 entities)

1. **[Entity 1 - e.g., User]**: id, email, name, password_hash
2. **[Entity 2 - e.g., Product]**: id, name, price, description, stock
3. **[Entity 3 - e.g., Order]**: id, user_id, status, total, items

---

## 6. Main Routes/Endpoints (Top 5-10)

| Path            | Description    | Auth? |
| --------------- | -------------- | ----- |
| `/`             | Home page      | No    |
| `/login`        | Login page     | No    |
| `/dashboard`    | User dashboard | Yes   |
| `/api/products` | List products  | No    |
| `/api/orders`   | Create order   | Yes   |

---

## 7. Domain Terminology (3-5 key terms)

1. **[Term 1 - e.g., User]**: [Person who purchases products]
2. **[Term 2 - e.g., Seller]**: [Person who lists products for sale]
3. **[Term 3 - e.g., Order]**: [A purchase transaction with payment]

---

## 8. Environment Setup

**Prerequisites**: [e.g., Node.js 20+, Docker, PostgreSQL]

**Quick Start**:

```bash
# [Install command - e.g., npm install]
# [Setup command - e.g., docker-compose up -d]
# [Migration command - e.g., npm run db:migrate]
# [Start command - e.g., npm run dev]
```

---

## 9. Testing Strategy

- **Unit Test Coverage**: [e.g., 80% business logic]
- **Integration Tests**: [e.g., All API endpoints]
- **E2E Tests**: [e.g., Critical user flows only]
- **Testing Philosophy**: [e.g., TDD, Test-after, None]

---

## 10. Architecture Notes

**Why this stack?**
[Brief explanation of why you chose these technologies]

**Key Constraints**:
[Any important technical or business constraints]

---

## Optional: Additional Information

### Third-Party Services (if used)

- Auth: [e.g., Clerk, None]
- Payment: [e.g., Stripe, None]
- Email: [e.g., SendGrid, None]

### Non-Functional Requirements

- Performance: [e.g., Page load < 2s]
- Security: [e.g., HTTPS, Auth required]
- Compliance: [e.g., GDPR, None]

---

**That's it!** The skill will use this information plus your codebase to generate comprehensive documentation.
