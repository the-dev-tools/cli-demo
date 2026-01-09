# DevTools Flow Demo

This project contains API flow tests for an e-commerce admin panel using DevTools CLI.

## Setup

1. **Set environment variables**

   The flow requires login credentials to be set as environment variables:

   ```bash
   export LOGIN_EMAIL="admin@example.com"
   export LOGIN_PASSWORD="admin123"
   ```

   Or create a `.env` file in the project root:

   ```bash
   LOGIN_EMAIL=admin@example.com
   LOGIN_PASSWORD=admin123
   ```

2. **Review the flow configuration**

   The flow is defined in `exported-dev-tools.yaml` and includes:
   - User authentication
   - CRUD operations for categories, products, and tags
   - API endpoint testing with assertions

## Running the Flow

Execute the flow with the following command:

```bash
devtools flow run exported-dev-tools.yaml
```

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

**Solution:** Make sure you've exported the required environment variables before running the flow.

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
