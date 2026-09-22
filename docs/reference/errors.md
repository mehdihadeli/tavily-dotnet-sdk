# Errors

The SDK exposes typed exceptions for common authentication, request, access,
quota, and transport failures.

| Exception                             | Typical cause                         |
| ------------------------------------- | ------------------------------------- |
| `MissingApiKeyException`              | No key could be resolved.             |
| `InvalidApiKeyException`              | Tavily rejected the API key.          |
| `BadRequestException`                 | Request validation failed.            |
| `ForbiddenException`                  | The key lacks access to an operation. |
| `UsageLimitExceededException`         | Account usage limit was reached.      |
| `TavilyKeylessLimitException`         | A keyless request hit a Tavily limit. |
| `TavilyTimeoutException`              | The Tavily request timed out.         |
| `KeylessUnsupportedEndpointException` | Operation requires authentication.    |

Handle these exceptions at your application boundary and preserve the original
exception when logging or translating errors.
