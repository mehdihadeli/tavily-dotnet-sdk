# API capabilities

The client maps Tavily operations to asynchronous methods with typed request
and response models. JSON names follow Tavily's snake-case API contract.

| Tavily operation       | Client method               |
| ---------------------- | --------------------------- |
| Search                 | `SearchAsync`               |
| Extract                | `ExtractAsync`              |
| Crawl                  | `CrawlAsync`                |
| Map                    | `MapAsync`                  |
| Submit research        | `ResearchAsync`             |
| Poll research          | `GetResearchAsync`          |
| Usage                  | `GetUsageAsync`             |
| Request logs           | `GetLogsAsync`              |
| Organization usage     | `GetOrganizationUsageAsync` |
| Feedback               | `SubmitFeedbackAsync`       |
| Search context         | `GetSearchContextAsync`     |
| Question-answer search | `QnaSearchAsync`            |
| Company information    | `GetCompanyInfoAsync`       |

## Extract, crawl, and map

```csharp
var extracted = await client.ExtractAsync(new TavilyExtractRequest
{
  Urls = ["https://learn.microsoft.com/dotnet/"],
  ExtractDepth = "advanced",
  Format = "markdown",
}, cancellationToken);

var crawl = await client.CrawlAsync(new TavilyCrawlRequest
{
  Url = "https://docs.tavily.com",
  MaxDepth = 2,
  Limit = 20,
}, cancellationToken);

var map = await client.MapAsync(new TavilyMapRequest
{
  Url = "https://docs.tavily.com",
  MaxDepth = 2,
  Limit = 20,
}, cancellationToken);
```

## Research

Research submission returns a request ID. Poll that ID for the completed result:

```csharp
var queued = await client.ResearchAsync(new TavilyResearchRequest
{
  Input = "Research the latest developments in AI",
  Model = "pro",
  CitationFormat = "apa",
}, cancellationToken);

var result = await client.GetResearchAsync(
  queued.RequestId!,
  cancellationToken,
  includeUsage: true);
```

The .NET SDK exposes polling through `GetResearchAsync`; it does not expose the
Python SDK's streaming research iterator.

For endpoint parameters and server behavior, see the [official Tavily API
reference](https://docs.tavily.com/documentation/api-reference).
