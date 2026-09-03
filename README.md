# Simple Login for Testing

A minimal static HTML authentication test application designed for **testRigor codeCake credential override testing**.

## About This Project

This repository contains a simple client-side login application with hardcoded credentials. It is purpose-built as a minimal test fixture for automated testing frameworks, specifically testRigor's codeCake feature for testing authentication credential overrides.

The application does not use any backend services, databases, or external authentication systems—it is purely a static HTML/CSS/JavaScript implementation for testing login flows locally.

## Default Credentials

| Email | Password | Expected Result |
|-------|----------|-----------------|
| `default@test.com` | `default123` | `WELCOME DEFAULT USER` |
| `override@test.com` | `override123` | `WELCOME OVERRIDE USER` |
| *any other* | *any other* | `INVALID CREDENTIALS` |

## How to Run

### Prerequisites

- [Docker](https://www.docker.com/products/docker-desktop) (includes Docker Compose)

### Starting the Application

1. **Navigate to the repository root:**
   ```bash
   cd simpleLoginForTesting
   ```

2. **Start the Docker Compose service:**
   ```bash
   docker-compose -f codeCake/docker-compose.yml up
   ```

   You should see output like:
   ```
   simplelogin-test  | 2024/XX/XX XX:XX:XX [notice] nginx/X.XX.X worker process started
   ```

3. **Open the application in your browser:**
   - **URL:** `http://localhost:8080`
   - The login page will load immediately

### Stopping the Application

To stop the Docker container, press `Ctrl+C` in your terminal, or run:

```bash
docker-compose -f codeCake/docker-compose.yml down
```

To remove the container completely:

```bash
docker-compose -f codeCake/docker-compose.yml down -v
```

## Architecture

- **Web Server:** nginx (Alpine Linux, minimal image)
- **Port:** `8080` (mapped to container port `80`)
- **Content:** Static HTML/CSS/JavaScript (no backend, no database)
- **Volume:** Repository root mounted as read-only to `/usr/share/nginx/html`

## Testing the Login Flow

1. **Default User Test:**
   - Email: `default@test.com`
   - Password: `default123`
   - Expected: Page displays "WELCOME DEFAULT USER"

2. **Override User Test:**
   - Email: `override@test.com`
   - Password: `override123`
   - Expected: Page displays "WELCOME OVERRIDE USER"

3. **Invalid Credentials Test:**
   - Email: `any@example.com`
   - Password: `anypassword`
   - Expected: Page displays "INVALID CREDENTIALS"

## Use with testRigor codeCake

This application is designed to test credential override functionality. You can:

1. Start the application with default credentials
2. Use testRigor codeCake to override the credentials at runtime
3. Verify that the override credentials are properly substituted during testing

The static nature of this application makes it ideal for testing credential injection mechanisms without the complexity of a real backend.

## Important Notes

⚠️ **Do not modify the `index.html` file**—it contains the core testing logic.

- The credentials are **hardcoded client-side** for testing purposes only
- This application is **not suitable for production use**
- All authentication happens **in the browser** (JavaScript)
- No network requests are made; everything is local

## Project Structure

```
simpleLoginForTesting/
├── index.html                 # Main login application (do not modify)
├── README.md                  # This file
└── codeCake/
    └── docker-compose.yml     # Docker Compose configuration
```

## Troubleshooting

### Port Already in Use

If port `8080` is already in use, you can modify the port mapping in `codeCake/docker-compose.yml`:

```yaml
ports:
  - "9090:80"  # Change 9090 to your desired port
```

Then access the application at `http://localhost:9090`

### Container Won't Start

Ensure Docker is running:
```bash
docker --version
docker-compose --version
```

### Cannot Access the Application

- Verify the container is running: `docker ps`
- Check logs: `docker logs simplelogin-test`
- Try opening `http://127.0.0.1:8080` instead of `localhost`

## License

This project is provided as-is for testing purposes.

## Netlify published: https://aquamarine-frangollo-5649fe.netlify.app/
