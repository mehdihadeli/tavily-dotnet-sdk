# Models and operations

Use the typed request models with `TavilyClient` or `ITavilyClient`.

## Core request models

- `TavilySearchRequest`
- `TavilyExtractRequest`
- `TavilyCrawlRequest`
- `TavilyMapRequest`
- `TavilyResearchRequest`
- `TavilyLogsRequest`
- `TavilyFeedbackRequest`
- `TavilySearchContextRequest`

## Administrative operations

`GetUsageAsync`, `GetLogsAsync`, and `GetOrganizationUsageAsync` expose usage
and request metadata for keys and organizations. Availability depends on the
Tavily plan and permissions associated with the key.

## Official API reference

SDK coverage follows the [Tavily OpenAPI specification](https://docs.tavily.com/documentation/api-reference/openapi.json).
