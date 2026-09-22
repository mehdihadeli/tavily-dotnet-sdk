# HTTP clients and cancellation

Inject `HttpClient` to control transport behavior without changing the SDK's
request models or authentication flow.

```csharp
using var httpClient = new HttpClient
{
  BaseAddress = new Uri("https://api.tavily.com/"),
  Timeout = TimeSpan.FromSeconds(90),
};

var client = new TavilyClient(httpClient, "tvly-YOUR_API_KEY");
```

Use the injected client to configure a handler, proxy, retry policy, or test
transport. The default base address is `https://api.tavily.com/`.

## Cancellation

Pass the same token from the application boundary through the API call:

```csharp
var response = await client.SearchAsync(
  new TavilySearchRequest { Query = "latest .NET release" },
  cancellationToken);
```

All asynchronous client operations accept an optional `CancellationToken`.
