# Template: Docker + OAuth2.1 + PostgreSQL

This is a template repository for creating MCP servers with OAuth2.1 authentication and PostgreSQL database, containerized with Docker.

## Features

- ✅ OAuth2.1 authentication with PKCE
- ✅ PostgreSQL database with connection pooling
- ✅ Docker containerization
- ✅ Production-ready setup
- ✅ User management and token refresh
- ✅ TypeScript with full type safety
- ✅ Express.js server

## Quick Start

```bash
# Clone this template
git clone https://github.com/granular-software/template-docker-oauth-postgresql.git my-mcp-server
cd my-mcp-server

# Install dependencies
npm install

# Copy environment file
cp env.example .env

# Start with Docker Compose
npm run docker:compose

# Or start development server
npm run dev
```

## Documentation

See the [README.md](README.md) file for detailed documentation.

## License

MIT License - see [LICENSE](LICENSE) file for details.
