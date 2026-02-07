# Environments

> **Note**: This is a template document. Adapt, modify, or remove sections based on your project's specific infrastructure, deployment strategy, and technology stack. Replace all placeholders in [brackets] with your actual environment configurations, tools, and procedures.

This document describes the two primary workload environments for the [Project Name] application: Development (local machine) and Production (deployed).

## Environment Overview

| Aspect              | Development (Local)                                | Production (Deployed)                        |
| ------------------- | -------------------------------------------------- | -------------------------------------------- |
| **Purpose**         | Local development and testing                      | Live user-facing application                 |
| **Database**        | [Database] in [Container/Local]                    | [Managed Database Service]                   |
| **Cache**           | [Cache Service] in [Container/Local]               | [Managed Cache Service]                      |
| **Storage**         | [Local Storage Solution]                           | [Cloud Storage Service]                      |
| **Server**          | [Dev Server] (default) or [Process Manager] (test) | Production build served by [Server]          |
| **Process Manager** | [Process Manager] optional (for testing)           | [Process Manager] with [clustering strategy] |
| **SSL**             | Not required                                       | Required (HTTPS)                             |
| **Assets**          | Served by [dev server]                             | Served by [CDN]                              |
| **Monitoring**      | Console logs, [monitoring tool] (if using)         | [Monitoring services list]                   |
| **Scaling**         | Single instance or [process manager] (for testing) | [Scaling strategy]                           |

---

## Development Environment (Local Machine)

### Purpose

The development environment runs entirely on a developer's local machine for:

- Feature development
- Bug fixes
- Local testing
- Database schema changes
- Debugging

### Architecture

```
[ASCII diagram showing local development architecture]
[Include: local server, databases, caches, storage emulation]
```

### Prerequisites

#### Required Software

- **[Runtime] [Version]+**: [Description]
- **[Package Manager] [Version]+**: [Description]
- **[Container Platform]**: For [services] containers
- **[Version Control]**: Version control

#### Optional Tools

- **[Database GUI]**: Visual database browser
- **[Database Tool]**: Database management tool
- **[IDE]**: Recommended code editor with extensions:
  - [Extension 1]
  - [Extension 2]
  - [Extension 3]
  - [Extension 4]

### Setup Instructions

#### Quick Setup (Recommended)

Use the automated setup script:

```bash
# Run automated setup
[setup command]
```

This will:

- [Setup step 1]
- [Setup step 2]
- [Setup step 3]
- [Setup step 4]
- [Setup step 5]
- [Setup step 6]

#### Manual Setup

If you prefer to set up manually:

#### 1. Clone Repository

```bash
git clone <repository-url>
cd [project-directory]
```

#### 2. Install Dependencies

```bash
[install command]
```

#### 3. Start [Database/Cache/Storage] Services

The `[container config file]` file is already provided in the project root. Start services:

```bash
# Start all services
[start services command]

# Or using [container tool] directly
[container start command]

# View logs
[logs command]
```

**Services included:**

- **[Service 1]** on port [port]
- **[Service 2]** on port [port]
- **[Service 3]** on port [port]

**Health checks:** All services include health checks to ensure they're ready before use.

Verify services are running:

```bash
# Check all containers
[check containers command]

# Test [Service 1]
[test service 1 command]

# Test [Service 2]
[test service 2 command]

# Test [Service 3]
[test service 3 command]
```

#### 4. Configure Environment Variables

Copy the example environment file:

```bash
cp [env example file] [env file]
```

The `[env example file]` file contains all necessary variables for local development with sensible defaults. Review and modify if needed:

```bash
# [Category 1]
[VAR_NAME]=[value]
[VAR_NAME]=[value]

# [Category 2]
[VAR_NAME]=[connection string]

# [Category 3]
[VAR_NAME]=[connection string]

# [Category 4]
[VAR_NAME]=[value]
[VAR_NAME]=[value]
[VAR_NAME]=[value]

# [Category 5]
[VAR_NAME]=[value]
```

#### 5. Set Up Database

```bash
# [Database setup command 1]
[command]

# [Database setup command 2]
[command]

# [Database setup command 3]
[command]
```

#### 6. Start Development Server

```bash
[dev server start command]
```

The application will be available at `[url]`

### Development Workflow

#### Daily Development

**Option 1: Using [Dev Server] (Recommended for active development)**

```bash
# Start services (if not running)
[start services command]

# Start dev server with [hot reload feature]
[dev server command]

# In another terminal: run tests in watch mode
[test command]
```

**Option 2: Using [Process Manager] (For testing production-like behavior)**

```bash
# Start services (if not running)
[start services command]

# Build and start with [process manager]
[process manager dev command]

# View logs
[logs command]

# Monitor resources
[monitoring command]

# Stop [process manager] when done
[stop command]
```

**When to use each approach:**

- **[Dev Server]** ([command]):
  - [Use case 1]
  - [Use case 2]
  - [Use case 3]
  - [Use case 4]

- **[Process Manager]** ([command]):
  - [Use case 1]
  - [Use case 2]
  - [Use case 3]
  - [Use case 4]
  - [Use case 5]

#### Database Changes

```bash
# Modify [database schema file]

# [Migration creation command]
[command]

# [Note about automatic steps]
```

#### View Database

```bash
# [Database GUI command]
[command]

# Or connect with your preferred tool:
# Host: [host]
# Port: [port]
# Database: [database name]
# User: [username]
# Password: [password]
```

#### Stop Services

```bash
# Stop containers (preserves data)
[stop command]

# Stop and remove all data
[clean command]

# Or using [container tool] directly
[container stop command]    # Stop only
[container down command]    # Stop and remove containers
[container down with volumes command] # Stop and delete all data
```

#### Helper Scripts

The project includes convenience scripts in the `[scripts directory]/` directory:

```bash
# [Script 1 description]
[command]

# [Script 2 description]
[command]
```

See `[scripts readme]` for more details.

### Development Best Practices

1. **Never commit [sensitive file]** - [Reason]
2. **Use meaningful [change descriptions]** - [Reason]
3. **[Best practice 3]** - [Reason]
4. **[Best practice 4]** - [Reason]
5. **[Best practice 5]** - [Reason]
6. **[Best practice 6]** - [Reason]
7. **[Best practice 7]** - [Reason]
8. **Choose the right dev server**:
   - Use [dev server] for [use case]
   - Use [process manager] for [use case]
9. **[Best practice 9]** - [Reason]

### Troubleshooting Development Environment

#### [Service 1] Connection Issues

```bash
# Check if [service] is running
[check command]

# Check [service] logs
[logs command]

# Verify connection
[verify command]
```

#### [Service 2] Connection Issues

```bash
# Check if [service] is running
[check command]

# Test connection
[test command]
# Should return: [expected output]

# Check [service] logs
[logs command]
```

#### [Service 3] Issues

```bash
# Check if [service] is running
[check command]

# Check [service] logs
[logs command]

# Test [service] connection
[test command]

# Recreate [resource] if needed
[recreate command]

# Test [operation]
[test operation commands]
```

#### [ORM/Database Client] Issues

```bash
# [Regenerate command]
[command]

# [Reset command] (WARNING: deletes all data)
[command]
```

#### Port Conflicts

If ports [port list] are already in use:

```yaml
# Edit [container config file] to use different ports
[service1]:
  ports:
    - '[new-port]:[old-port]' # Changed from [old-port]

[service2]:
  ports:
    - '[new-port]:[old-port]' # Changed from [old-port]
```

Update `[env file]` accordingly:

```bash
[CONNECTION_STRING]="[updated connection string with new port]"
[CONNECTION_STRING]="[updated connection string with new port]"
```

#### [Process Manager] Development Issues

**[Process manager] processes not stopping:**

```bash
# Force delete all [process manager] processes
[delete command]

# Or kill [process manager] daemon and restart
[kill command]
[restart command]
```

**Port already in use ([port]):**

If [dev server] is still running:

```bash
# Find process using port [port]
[find process command]

# Or stop [process manager] if it's running
[stop command]
```

**[Process Manager] and [Dev Server] conflict:**

Don't run both simultaneously. Choose one:

```bash
# If using [dev server]
[dev server command]

# If switching to [process manager], first stop [dev server], then:
[process manager command]

# When done with [process manager], clean up before using [dev server] again
[cleanup command]
[dev server command]
```

---

## Production Environment (Deployed)

### Purpose

The production environment hosts the live application accessible to users:

- Serves real users
- Handles production traffic
- Stores real user data
- Requires high availability and security
- Monitored 24/7

### Architecture

```
[ASCII diagram showing production architecture]
[Include: DNS, CDN, load balancers, application servers, databases, caches, storage]
```

### Infrastructure Components

#### Process Management ([Process Manager])

**Production Process Manager:** [Process Manager] is used to manage [application] processes in production, providing:

- **[Feature 1]**: [Description]
- **[Feature 2]**: [Description]
- **[Feature 3]**: [Description]
- **[Feature 4]**: [Description]
- **[Feature 5]**: [Description]
- **[Feature 6]**: [Description]
- **[Feature 7]**: [Description]

**Installation:**

```bash
# Install [process manager] globally
[install command]

# Or install as project dependency (already included in [package file])
[local install command]
```

**[Process Manager] Configuration:**

The application includes `[config file]` for [process manager] configuration:

- **[Config 1]**: [Description]
- **[Config 2]**: [Description]
- **[Config 3]**: [Description]
- **[Config 4]**: [Description]
- **[Config 5]**: [Description]

**[Process Manager] Commands:**

```bash
# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]
```

**[Process Manager] Monitoring:**

[Process Manager] provides real-time monitoring of:

- [Metric 1]
- [Metric 2]
- [Metric 3]
- [Metric 4]
- [Metric 5]
- [Metric 6]

**[Process Manager] Plus (Optional):**

For advanced monitoring and management:

```bash
# [Connect command]
[command]
```

Features include:

- [Feature 1]
- [Feature 2]
- [Feature 3]
- [Feature 4]
- [Feature 5]

#### Application Layer

**Options:**

- **[Deployment Option 1]**: [Description]
- **[Deployment Option 2]**: [Description]
- **[Deployment Option 3]**: [Description]

**Configuration:**

- [Configuration detail 1]
- [Configuration detail 2]
- [Configuration detail 3]
- [Configuration detail 4]

#### Database Layer ([Database])

**Service:** [Managed Database Service] or self-managed

**Configuration:**

```
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
```

**Connection Pooling:**

```[language]
// Production [database client] configuration
[connection configuration code]

// Environment variable format:
// [CONNECTION_STRING]="[connection string with pooling parameters]"
```

#### Cache Layer ([Cache Service])

**Service:** [Managed Cache Service] or self-managed

**Configuration:**

```
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
```

#### Storage Layer ([Storage Service])

**Service:** [Cloud Storage Service]

**Configuration:**

```
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
```

**Use Cases:**

- [Use case 1]
- [Use case 2]
- [Use case 3]
- [Use case 4]

**Access Pattern:**

```[language]
// [Description of access pattern]
[code example showing access pattern]
```

#### CDN ([CDN Service])

**Purpose:**

- [Purpose 1]
- [Purpose 2]
- [Purpose 3]
- [Purpose 4]

**Configuration:**

```
[Config section]:
  - [Config detail]
  - [Config detail]
[Config section]:
  - [Config detail]
  - [Config detail]
[Config section]: [Config value]
[Config section]: [Config value]
```

#### Load Balancer

**Type:** [Load Balancer Type]

**Configuration:**

```
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
[Config Key]: [Config Value]
```

### Environment Variables (Production)

**Secure Storage:** [Secret Management Service]

```bash
# [Category 1]
[VAR_NAME]=[value]
[VAR_NAME]=[value]

# [Category 2]
# [Subcategory]
[VAR_NAME]=[connection string]

# [Subcategory]
[VAR_NAME]=[connection string]

# [Category 3]
[VAR_NAME]=[connection string]

# [Category 4]
[VAR_NAME]=[value]
[VAR_NAME]=[value]
# [Note about credentials]

# [Category 5]
[VAR_NAME]=[value]

# [Category 6]
[VAR_NAME]=[value]

# [Category 7]
[VAR_NAME]=[value]
[VAR_NAME]=[value]

# [Category 8]
[VAR_NAME]=[value]
[VAR_NAME]=[value]
```

### Deployment Process

#### 1. Pre-deployment Checks

```bash
# Run all tests
[test commands]

# Build application
[build command]

# Check build output
[check output command]
```

#### 2. Database Migrations

```bash
# Apply migrations to production database
# Run during maintenance window or use zero-downtime strategies
[migration command]
```

**Zero-Downtime Migration Strategy:**

1. [Strategy step 1]
2. [Strategy step 2]
3. [Strategy step 3]
4. [Strategy step 4]

#### 3. Build and Push [Container] Image

```dockerfile
# [Container file name]
[Dockerfile content showing build stages]
```

Build and push:

```bash
# Build image
[build command]

# Tag for registry
[tag command]

# Push to registry
[push command]
```

#### 4. Deploy to Production

**Using [Deployment Platform 1]:**

```bash
# [Deployment commands and description]
[commands]
```

**Using [Deployment Platform 2]:**

```bash
# [Deployment commands and description]
[commands]
```

**Using [Deployment Platform 3]:**

```bash
# [Deployment commands]
[commands]
```

#### 5. Post-deployment Verification

```bash
# Check application health
[health check command]

# Verify database migrations
[migration status command]

# Monitor error rates in [APM]
# Check [monitoring service] metrics
# Review application logs
```

#### 6. Rollback Plan

```bash
# If issues detected, rollback to previous version
[rollback commands for different platforms]
```

### Production Monitoring

#### Metrics to Monitor

**Application Metrics:**

- [Metric 1]
- [Metric 2]
- [Metric 3]
- [Metric 4]

**Database Metrics:**

- [Metric 1]
- [Metric 2]
- [Metric 3]
- [Metric 4]

**Cache Metrics:**

- [Metric 1]
- [Metric 2]
- [Metric 3]
- [Metric 4]

#### Logging

**Log Aggregation:** [Log Aggregation Service]

**Log Levels:**

- **[LEVEL]**: [Description]
- **[LEVEL]**: [Description]
- **[LEVEL]**: [Description]
- **[LEVEL]**: [Description]

**Structured Logging Example:**

```[language]
// Use structured logging
[code example showing structured logging]
```

#### Alerting

**Critical Alerts:**

- [Alert 1]
- [Alert 2]
- [Alert 3]
- [Alert 4]
- [Alert 5]

**Warning Alerts:**

- [Alert 1]
- [Alert 2]
- [Alert 3]
- [Alert 4]

### Security Considerations

#### SSL/TLS

- [Security measure 1]
- [Security measure 2]
- [Security measure 3]

#### Secrets Management

- [Security measure 1]
- [Security measure 2]
- [Security measure 3]
- [Security measure 4]

#### Network Security

- [Security measure 1]
- [Security measure 2]
- [Security measure 3]
- [Security measure 4]

#### Database Security

- [Security measure 1]
- [Security measure 2]
- [Security measure 3]
- [Security measure 4]
- [Security measure 5]

### Backup and Disaster Recovery

#### Database Backups

- **[Backup Type 1]**: [Description]
- **[Backup Type 2]**: [Description]
- **[Backup Type 3]**: [Description]
- **[Backup Type 4]**: [Description]

#### Backup Testing

```bash
# [Backup testing procedure]
# [Verification step]
# [Recovery time documentation]
# [Team training]
```

#### Recovery Time Objective (RTO)

- **Target RTO**: [Time] ([Description])
- **Target RPO**: [Time] ([Description])

### Scaling Strategy

#### Horizontal Scaling

**Auto-scaling Configuration:**

```yaml
[Config Key]: [Value]
[Config Key]: [Value]
[Config Key]: [Value]
[Config Key]: [Value]
[Config Key]: [Value]
[Config Key]: [Value]
```

#### Database Scaling

**Read Scaling:**

- [Strategy 1]
- [Strategy 2]

**Write Scaling:**

- [Strategy 1]
- [Strategy 2]
- [Strategy 3]

#### Cache Scaling

- [Strategy 1]
- [Strategy 2]
- [Strategy 3]

---

## Comparison: Development vs Production

### Configuration Differences

| Setting            | Development  | Production    |
| ------------------ | ------------ | ------------- |
| **[ENV_VAR]**      | [dev value]  | [prod value]  |
| **Database**       | [dev setup]  | [prod setup]  |
| **Cache**          | [dev setup]  | [prod setup]  |
| **Storage**        | [dev setup]  | [prod setup]  |
| **SSL**            | [dev config] | [prod config] |
| **Source Maps**    | [dev config] | [prod config] |
| **Hot Reload**     | [dev config] | [prod config] |
| **Minification**   | [dev config] | [prod config] |
| **Logging**        | [dev config] | [prod config] |
| **Error Handling** | [dev config] | [prod config] |

### Migration Path: Dev → Production

```
1. [Stage 1]
   ↓ ([action])
2. [Stage 2]
   ↓ ([condition])
3. [Stage 3]
   ↓ ([condition])
4. [Stage 4]
   ↓
5. [Stage 5]
```

### Environment Parity

**[Methodology] Principles:**

- [Principle 1]
- [Principle 2]
- [Principle 3]
- [Principle 4]
- [Principle 5]
- [Principle 6]

**Differences to Accept:**

- [Difference 1]
- [Difference 2]
- [Difference 3]

---

## Best Practices

### Development Environment

1. ✅ [Best practice 1]
2. ✅ [Best practice 2]
3. ✅ [Best practice 3]
4. ✅ [Best practice 4]
5. ✅ [Best practice 5]
6. ✅ [Best practice 6]
7. ✅ [Best practice 7]

### Production Environment

1. ✅ [Best practice 1]
2. ✅ [Best practice 2]
3. ✅ [Best practice 3]
4. ✅ [Best practice 4]
5. ✅ [Best practice 5]
6. ✅ [Best practice 6]
7. ✅ [Best practice 7]
8. ✅ [Best practice 8]
9. ✅ [Best practice 9]
10. ✅ [Best practice 10]

---

## Troubleshooting

### Common Production Issues

#### [Issue 1]

**Symptoms:** [Symptoms description]

**Solutions:**

- [Solution 1]
- [Solution 2]
- [Solution 3]
- [Solution 4]
- [Solution 5]
- [Solution 6]

#### [Issue 2]

**Symptoms:** [Symptoms description]

**Solutions:**

- [Solution 1]
- [Solution 2]
- [Solution 3]
- [Solution 4]

#### [Issue 3]

**Symptoms:** [Symptoms description]

**Solutions:**

- [Solution 1]
- [Solution 2]
- [Solution 3]
- [Solution 4]

### Getting Help

**For Development Issues:**

- [Resource 1]
- [Resource 2]
- [Resource 3]

**For Production Issues:**

- [Resource 1]
- [Resource 2]
- [Resource 3]
- [Resource 4]
- [Resource 5]

---

## Appendix

### Continuous Integration ([CI Platform])

The project uses [CI Platform] for automated testing and deployment on every commit.

**Pipeline stages:**

1. **[Stage 1]** - [Description]
2. **[Stage 2]**:
   - [Step 1]
   - [Step 2]
   - [Step 3]
3. **[Stage 3]** - [Description]
4. **[Stage 4]** - [Description]

**Key features:**

- [Feature 1]
- [Feature 2]
- [Feature 3]
- [Feature 4]
- [Feature 5]

See `[CI config documentation]` for detailed configuration documentation.

### Useful Commands

#### Development

```bash
# [Command description]
[command]

# [Command description]
[multi-line command sequence]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]
```

#### Production

```bash
# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]

# [Command description]
[command]
```

### Environment Variables Reference

See individual sections above for complete environment variable lists.

### Resources

- [Resource 1 with link]
- [Resource 2 with link]
- [Resource 3 with link]
- [Resource 4 with link]
