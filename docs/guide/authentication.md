# Authentication

The client sends the resolved Tavily key as a bearer token. Explicit
constructor values take precedence over environment and `.env` values.

## Explicit key

```csharp
var client = new TavilyClient(
  new HttpClient(),
  "tvly-YOUR_API_KEY");
```

## Environment variable

Set `TAVILY_API_KEY` before starting your application:

```bash
TAVILY_API_KEY=tvly-YOUR_API_KEY
```

Then construct the client without a key:

```csharp
var client = new TavilyClient(new HttpClient());
```

## Local `.env` file

For local development, the client searches for `.env` from the current
directory upward through its parent directories.

```text
TAVILY_API_KEY=tvly-YOUR_API_KEY
```

Keep `.env` outside shared source folders and add it to `.gitignore`. The SDK
does not support keyless mode; a missing key throws `MissingApiKeyException`.
