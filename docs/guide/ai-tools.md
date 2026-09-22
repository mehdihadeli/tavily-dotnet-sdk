# AI tool wrappers

The package provides `Microsoft.Extensions.AI` `AIFunction` wrappers for
search and extraction. They use the same authenticated `TavilyClient`.

```csharp
using Microsoft.Extensions.AI;

AIFunction searchTool = client.AsSearchTool();
AIFunction extractTool = client.AsExtractTool();
```

Set common search controls while creating the tool:

```csharp
AIFunction searchTool = client.AsSearchTool(
  maxResults: 5,
  searchDepth: "basic",
  includeAnswer: true);
```

Pass the resulting functions to the agent or chat client that supports
`AIFunction` tools. Tool execution remains subject to the same API key,
timeout, cancellation, and Tavily account limits as direct client calls.
