# Server Project Specification Template

> **Instructions**: Fill in the essential information below. The skill will gather additional details from your codebase as needed.

---

## 1. Project Basics

- **Project Name**: [Your project name]
- **Project Type**: [e.g., REST API, GraphQL API, Microservice, gRPC Service]
- **Description**: [1-2 sentence description]
- **Core Problem Solved**: [What problem does this solve?]

---

## 2. Technology Stack

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
- **Cloud/Hosting**: [e.g., AWS, Railway, Self-hosted]

### Observability

- **Logging**: [e.g., Winston, Pino, Morgan, Python logging]
- **Monitoring**: [e.g., DataDog, New Relic, Prometheus, None]
- **Error Tracking**: [e.g., Sentry, Rollbar, None]

### Testing & Tools

- **Unit/Integration Test**: [e.g., Vitest, Jest, Pytest, JUnit]
- **API Testing**: [e.g., Supertest, Postman, REST Client]
- **Package Manager**: [e.g., npm, pnpm, pip, yarn, cargo]

---

## 3. Key Features (3-5 main features)

1. [Feature 1 - e.g., User authentication and authorization]
2. [Feature 2 - e.g., Product catalog API with search]
3. [Feature 3 - e.g., Order processing and management]
4. [Feature 4 - e.g., Real-time notifications]
5. [Feature 5 - e.g., Admin API endpoints]

---

## 4. Core API Flows (Top 2-3)

**Flow 1: [e.g., User Authentication Flow]**

1. [Step 1 - e.g., Client sends credentials to /api/auth/login]
2. [Step 2 - e.g., Server validates credentials and generates JWT]
3. [Step 3 - e.g., Client receives token and uses for subsequent requests]

**Flow 2: [e.g., Order Creation Flow]**

1. [Step 1 - e.g., Client sends order data to /api/orders]
2. [Step 2 - e.g., Server validates, processes payment, creates order]
3. [Step 3 - e.g., Background job sends confirmation email]

---

## 5. Data Models (Top 3-5 entities)

1. **[Entity 1 - e.g., User]**: id, email, name, password_hash, role, created_at
2. **[Entity 2 - e.g., Product]**: id, name, price, description, stock, category_id
3. **[Entity 3 - e.g., Order]**: id, user_id, status, total, items, created_at

---

## 6. API Endpoints (Top 5-10)

| Method | Path              | Description       | Auth? |
| ------ | ----------------- | ----------------- | ----- |
| POST   | `/api/auth/login` | User login        | No    |
| GET    | `/api/products`   | List products     | No    |
| GET    | `/api/products/:id` | Get product     | No    |
| POST   | `/api/orders`     | Create order      | Yes   |
| GET    | `/api/orders/:id` | Get order         | Yes   |
| PUT    | `/api/users/:id`  | Update user       | Yes   |

---

## 7. Domain Terminology (3-5 key terms)

1. **[Term 1 - e.g., User]**: [Authenticated account holder]
2. **[Term 2 - e.g., Seller]**: [Person who lists products for sale]
3. **[Term 3 - e.g., Order]**: [A purchase transaction with payment]

---

## 8. Testing Strategy

- **Unit Test Coverage**: [e.g., 80% business logic]
- **Integration Tests**: [e.g., All API endpoints]
- **Load Testing**: [e.g., Critical endpoints only]
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

**Architecture Pattern**: [e.g., Layered, Clean Architecture, Hexagonal, MVC]

---

## 11. Optional: Additional Information

### Third-Party Services (if used)

- **Auth**: [e.g., Clerk, Auth0, None]
- **Payment**: [e.g., Stripe, PayPal, None]
- **Email**: [e.g., SendGrid, Resend, Mailgun, None]
- **SMS**: [e.g., Twilio, None]
- **Analytics**: [e.g., Google Analytics, Mixpanel, None]

### Non-Functional Requirements

- **Performance**: [e.g., API response < 200ms p95]
- **Scalability**: [e.g., Handle 10k concurrent requests]
- **Availability**: [e.g., 99.9% uptime]
- **Security**: [e.g., HTTPS, Rate limiting, Auth required]
- **Compliance**: [e.g., GDPR, HIPAA, SOC2, None]

### Deployment

- **CI/CD**: [e.g., GitHub Actions, GitLab CI, None]
- **Deployment Strategy**: [e.g., Blue-green, Rolling, Direct]
- **Environment Stages**: [e.g., Dev, Staging, Production]

---

**That's it!** The skill will use this information plus your codebase to generate comprehensive documentation.
