# DevTools Flow Demo

This project contains API flow tests for an e-commerce admin panel using DevTools CLI.

## 🚀 Quick Start

This flow is **designed for GitHub Actions** and automatically receives credentials from GitHub Secrets. Simply configure your secrets and push - no manual setup required!

## GitHub Actions Integration

**⚠️ IMPORTANT:** Environment variables are automatically injected from GitHub Secrets when running in GitHub Actions.

The flow uses the following environment variables that are **automatically injected from GitHub Secrets**:
- `LOGIN_EMAIL` - Admin email for authentication
- `LOGIN_PASSWORD` - Admin password for authentication

No manual configuration is needed when running in GitHub Actions - the secrets are automatically available to the workflow.

## Setup

### GitHub Secrets Configuration

To run this flow in GitHub Actions, ensure the following secrets are configured in your repository:

1. Go to your repository settings
2. Navigate to **Secrets and variables** → **Actions**
3. Add the following repository secrets:
   - `LOGIN_EMAIL` - Your admin email
   - `LOGIN_PASSWORD` - Your admin password

### Running Locally

If you need to run the flow locally for testing, follow these steps:

#### Prerequisites

Install DevTools CLI:

```bash
# Install DevTools CLI
curl -fsSL https://sh.dev.tools/install.sh | bash

# Verify installation
devtools --version

# View available commands
devtools --help
```

#### Step-by-Step Local Execution

```bash
# 1. Clone the repository
git clone https://github.com/the-dev-tools/cli-demo.git
cd cli-demo

# 2. Set environment variables (required for authentication)
export LOGIN_EMAIL="admin@example.com"
export LOGIN_PASSWORD="admin123"

# 3. Run the flow
devtools flow run exported-dev-tools.yaml

# Optional: Run with JUnit report output
devtools flow run --report console --report junit:test-results.xml exported-dev-tools.yaml

# Optional: Run with quiet mode (minimal output for CI/CD)
devtools flow run --quiet exported-dev-tools.yaml
```

### Flow Configuration

The flow is defined in `exported-dev-tools.yaml` and includes:
- User authentication
- CRUD operations for categories, products, and tags
- API endpoint testing with assertions

## Running the Flow

### In GitHub Actions (Recommended)

The flow runs automatically on every push to `main` branch via the workflow defined in `.github/workflows/flow-run.yml`.

The workflow automatically:
1. Checks out the repository
2. Injects `LOGIN_EMAIL` and `LOGIN_PASSWORD` from GitHub Secrets as environment variables
3. Installs DevTools CLI: `curl -fsSL https://sh.dev.tools/install.sh | bash`
4. Executes the flow with reporting: `devtools flow run --report console --report junit:test-results.xml exported-dev-tools.yaml`
5. Uploads the JUnit test results as artifacts
6. Publishes test results in the GitHub UI

**No manual configuration needed** - just configure your GitHub Secrets and push to the repository!

For local execution instructions, see the [Running Locally](#running-locally) section above.

### Expected Output

When the flow runs successfully, you should see:

```
=== Multi-Flow Execution Starting ===
Flows to execute: 1

[1/1] Executing flow: Imported HAR Flow
===========================================================
| Flow: Imported HAR Flow                                 |
───────────────────────────────────────────────────────────
| Timestamp            | Step    | Duration | Status      |
───────────────────────────────────────────────────────────
| ...                  | Start   | ...      | ✅ Success   |
| ...                  | http_1  | ...      | ✅ Success   |
...
===========================================================
Flow Duration: ~3s | Steps: 17/17 Successful
   ✅ Flow completed successfully

Flows completed: 1/1
```

## Flow Structure

The flow performs the following operations:

1. **Authentication** - Login to get access token
2. **GET requests** - Fetch categories, products, and tags
3. **POST requests** - Create new categories, products, and tags
4. **DELETE requests** - Clean up created resources

All requests use the authentication token obtained from the login step.

## Troubleshooting

### Environment variable not found

```
ERROR: environment variable LOGIN_EMAIL: key not found
```

**In GitHub Actions:** Verify that the secrets `LOGIN_EMAIL` and `LOGIN_PASSWORD` are configured in your repository settings.

**Locally:** Make sure you've exported the required environment variables before running the flow.

### Connection errors

```
ERROR: connection refused
```

**Solution:** Verify that the API endpoint (`https://ecommerce-admin-panel.fly.dev`) is accessible from your network.

### Authentication failures

```
ERROR: response.status == 200 assertion failed
```

**Solution:** Check that your login credentials are correct.

## API Endpoint

The flow connects to: `https://ecommerce-admin-panel.fly.dev`

You can modify the API endpoint in the `environments` section of `exported-dev-tools.yaml`:

```yaml
environments:
  - name: default
    variables:
      api: https://your-custom-endpoint.com
```
