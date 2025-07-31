# {{PROJECT_NAME}}

{{PROJECT_DESCRIPTION}}

This template provides a production-ready MCP server with OAuth2.1 authentication and PostgreSQL database, containerized with Docker.

## Features

- ✅ OAuth2.1 authentication with PKCE
- ✅ PostgreSQL database with connection pooling
- ✅ Docker containerization
- ✅ Production-ready setup
- ✅ User management and token refresh
- ✅ TypeScript with full type safety
- ✅ Express.js server

## Quick Start

### Prerequisites

- Docker and Docker Compose
- PostgreSQL database (local or cloud)

### 1. Clone and Setup

```bash
# Clone this template
git clone https://github.com/granular-software/template-docker-oauth-postgresql.git my-mcp-server
cd my-mcp-server

# Install dependencies
npm install
```

### 2. Environment Configuration

Copy the example environment file and configure it:

```bash
cp .env.example .env
```

Edit `.env` with your configuration:

```env
# Database Configuration
DATABASE_URL=postgresql://username:password@localhost:5432/mcpresso

# OAuth Configuration
JWT_SECRET=your-secure-secret-key-here

# Server Configuration
SERVER_URL=https://your-server.com
PORT=3000
```

### 3. Database Setup

#### Option A: Local PostgreSQL with Docker Compose

```bash
# Start PostgreSQL with Docker Compose
npm run docker:compose

# The database will be available at localhost:5432
# Default credentials: postgres/postgres
```

#### Option B: External PostgreSQL

Use your own PostgreSQL instance and update the `DATABASE_URL` in `.env`.

### 4. Development

```bash
# Start development server
npm run dev

# The server will be available at http://localhost:3000
# MCP Inspector: http://localhost:3000
```

### 5. Production Deployment

```bash
# Build the Docker image
npm run docker:build

# Run with Docker
npm run docker:run

# Or use Docker Compose for full stack
npm run docker:compose
```

## Project Structure

```
├── src/
│   ├── server.ts              # Main server file
│   ├── auth/
│   │   └── oauth.ts          # OAuth configuration
│   ├── storage/
│   │   └── postgres-storage.ts # PostgreSQL storage implementation
│   ├── data/
│   │   └── users.ts          # Demo users
│   └── resources/
│       └── example.ts        # Example MCP resource
├── docker-compose.yml         # Docker Compose configuration
├── Dockerfile                 # Docker image definition
├── .env.example              # Environment variables template
└── README.md                 # This file
```

## OAuth2.1 Authentication

This template includes a complete OAuth2.1 implementation with:

- **PKCE (Proof Key for Code Exchange)** for enhanced security
- **Dynamic client registration** - no pre-configured credentials needed
- **User management** with PostgreSQL storage
- **Token refresh** functionality
- **Customizable login page**

### Demo Users

The template includes demo users for testing:

- **alice@example.com** / `alice123` (read, write permissions)
- **bob@example.com** / `bob123` (read permissions only)

### OAuth Flow

1. Client registers dynamically with the server
2. User authenticates via the login page
3. Authorization code is issued with PKCE
4. Access token is exchanged for the code
5. API calls use the access token

## Database Schema

The PostgreSQL storage automatically creates the following tables:

- `oauth_clients` - Registered OAuth clients
- `oauth_users` - User accounts
- `oauth_authorization_codes` - Authorization codes
- `oauth_access_tokens` - Access tokens
- `oauth_refresh_tokens` - Refresh tokens

## Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `DATABASE_URL` | PostgreSQL connection string | Yes | - |
| `JWT_SECRET` | Secret key for JWT tokens | Yes | - |
| `SERVER_URL` | Base URL of your server | Yes | - |
| `PORT` | Server port | No | 3000 |

## Development

### Adding Resources

Create new MCP resources in `src/resources/`:

```typescript
import { z } from "zod";
import { createResource } from "mcpresso";

const MyResourceSchema = z.object({
  id: z.string(),
  name: z.string(),
  // ... your schema
});

export const myResource = createResource({
  name: "my-resource",
  schema: MyResourceSchema,
  uri_template: "my-resources/{id}",
  methods: {
    get: {
      handler: async ({ id }) => {
        // Your implementation
      },
    },
    // ... other methods
  },
});
```

### Customizing OAuth

Edit `src/auth/oauth.ts` to customize:

- Login page styling
- User authentication logic
- Supported scopes and grant types
- Token expiration times

## Production Considerations

1. **Security**: Change all default secrets and passwords
2. **Database**: Use a managed PostgreSQL service for production
3. **SSL**: Ensure HTTPS is enabled in production
4. **Monitoring**: Add logging and monitoring
5. **Backup**: Implement database backup strategy

## Troubleshooting

### Common Issues

1. **Database Connection**: Ensure PostgreSQL is running and accessible
2. **Port Conflicts**: Change `PORT` in `.env` if 3000 is in use
3. **Docker Issues**: Ensure Docker is running and has sufficient resources

### Logs

Check logs for debugging:

```bash
# Application logs
npm run dev

# Docker logs
docker-compose logs

# Database logs
docker-compose logs postgres
```

## License

MIT License - see LICENSE file for details.

## Support

- GitHub Issues: https://github.com/granular-software/mcpresso
- Documentation: https://github.com/granular-software/mcpresso 