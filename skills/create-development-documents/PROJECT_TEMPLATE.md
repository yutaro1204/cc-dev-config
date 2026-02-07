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

### Frontend

- **Framework**: [e.g., React Router v7, Next.js, Vue, Angular, None]
- **Language**: [e.g., TypeScript, JavaScript]
- **State Management**: [e.g., React Context, Redux, Zustand, None]
- **Styling**: [e.g., Tailwind CSS, CSS Modules, SCSS]
- **Build Tool**: [e.g., Vite, Webpack, Turbopack]

### Backend

- **Framework**: [e.g., Express, NestJS, Django, FastAPI, Rails]
- **Language**: [e.g., TypeScript, Python, Java, Go, Rust]
- **API Type**: [e.g., REST, GraphQL, tRPC, gRPC]
- **Database**: [e.g., PostgreSQL, MongoDB, MySQL, SQLite]
- **ORM/Query Builder**: [e.g., Prisma, TypeORM, Drizzle, SQLAlchemy, Mongoose]
- **Authentication**: [e.g., JWT, Session-based, OAuth2, Passport.js, Auth.js]
- **Validation**: [e.g., Zod, Joi, class-validator, Pydantic]

### Infrastructure & Services

- **Cache**: [e.g., Redis, Valkey, Memcached, None]
- **Message Queue**: [e.g., BullMQ, RabbitMQ, Kafka, None]
- **Background Jobs**: [e.g., BullMQ, Celery, Sidekiq, None]
- **Storage**: [e.g., S3, Local, Cloud Storage, None]
- **Search**: [e.g., Elasticsearch, Algolia, MeiliSearch, None]
- **Container**: [e.g., Docker Compose, Kubernetes, None]
- **Cloud/Hosting**: [e.g., AWS, Vercel, Railway, Self-hosted]

### Observability

- **Logging**: [e.g., Winston, Pino, Morgan, Python logging]
- **Monitoring**: [e.g., DataDog, New Relic, Prometheus, None]
- **Error Tracking**: [e.g., Sentry, Rollbar, None]

### Testing & Tools

- **Unit/Integration Test**: [e.g., Vitest, Jest, Pytest, JUnit]
- **E2E Framework**: [e.g., Playwright, Cypress, None]
- **API Testing**: [e.g., Supertest, Postman, REST Client]
- **Package Manager**: [e.g., npm, pnpm, pip, yarn, cargo]

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

### Frontend Routes (if applicable)

| Path         | Description    | Auth? |
| ------------ | -------------- | ----- |
| `/`          | Home page      | No    |
| `/login`     | Login page     | No    |
| `/dashboard` | User dashboard | Yes   |

### API Endpoints

| Method | Path              | Description    | Auth? |
| ------ | ----------------- | -------------- | ----- |
| GET    | `/api/products`   | List products  | No    |
| POST   | `/api/orders`     | Create order   | Yes   |
| GET    | `/api/orders/:id` | Get order      | Yes   |
| PUT    | `/api/users/:id`  | Update user    | Yes   |

---

## 7. Domain Terminology (3-5 key terms)

1. **[Term 1 - e.g., User]**: [Person who purchases products]
2. **[Term 2 - e.g., Seller]**: [Person who lists products for sale]
3. **[Term 3 - e.g., Order]**: [A purchase transaction with payment]

---

## 8. Testing Strategy

- **Unit Test Coverage**: [e.g., 80% business logic]
- **Integration Tests**: [e.g., All API endpoints]
- **E2E Tests**: [e.g., Critical user flows only]
- **Testing Philosophy**: [e.g., TDD, Test-after, None]

---

## 9. Backend Configuration

### API Design

- **API Style**: [e.g., RESTful, GraphQL, tRPC]
- **API Versioning**: [e.g., URL-based /api/v1, Header-based, None]
- **Response Format**: [e.g., JSON, Protocol Buffers]
- **Error Format**: [e.g., RFC 7807, Custom error codes]
- **Pagination**: [e.g., Offset-based, Cursor-based, None]

### Security

- **CORS Policy**: [e.g., Specific origins, Wildcard for dev]
- **Rate Limiting**: [e.g., 100 req/min per IP, None]
- **Input Validation**: [e.g., Zod schemas on all endpoints]
- **HTTPS**: [e.g., Required in production, None]
- **API Keys/Tokens**: [e.g., Bearer tokens, API keys, None]

### Data Processing

- **File Uploads**: [e.g., Direct to S3, Local storage, None]
- **Background Jobs**: [e.g., Email sending, Report generation, None]
- **Scheduled Tasks**: [e.g., Daily cleanup, Weekly reports, None]
- **Webhooks**: [e.g., Payment callbacks, None]

### Database Strategy

- **Migration Strategy**: [e.g., Automatic on deploy, Manual review]
- **Seeding**: [e.g., Dev data included, Production data separate]
- **Backup**: [e.g., Daily automated, None]
- **Indexing Strategy**: [e.g., On foreign keys and search fields]

---

## 10. Architecture Notes

**Why this stack?**
[Brief explanation of why you chose these technologies]

**Key Constraints**:
[Any important technical or business constraints]

**Separation of Concerns**: [e.g., Monorepo, Separate repos, Monolith]

---

## 11. Optional: Additional Information

### Third-Party Services (if used)

- **Auth**: [e.g., Clerk, Auth0, None]
- **Payment**: [e.g., Stripe, PayPal, None]
- **Email**: [e.g., SendGrid, Resend, Mailgun, None]
- **SMS**: [e.g., Twilio, None]
- **Analytics**: [e.g., Google Analytics, Mixpanel, None]
- **CDN**: [e.g., CloudFlare, CloudFront, None]

### Non-Functional Requirements

- **Performance**: [e.g., API response < 200ms p95, Page load < 2s]
- **Scalability**: [e.g., Handle 10k concurrent users]
- **Availability**: [e.g., 99.9% uptime]
- **Security**: [e.g., HTTPS, Rate limiting, Auth required]
- **Compliance**: [e.g., GDPR, HIPAA, SOC2, None]

### Deployment

- **CI/CD**: [e.g., GitHub Actions, GitLab CI, None]
- **Deployment Strategy**: [e.g., Blue-green, Rolling, Direct]
- **Environment Stages**: [e.g., Dev, Staging, Production]

---

**That's it!** The skill will use this information plus your codebase to generate comprehensive documentation.
