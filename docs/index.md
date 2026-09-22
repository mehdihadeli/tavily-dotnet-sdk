---
layout: home
title: Tavily .NET SDK
titleTemplate: Typed Tavily API access
description: Search, extract, crawl, map, and research from .NET with typed requests and responses.
hero:
  name: Tavily .NET SDK
  text: Tavily API access, typed for .NET
  tagline: Build search and research workflows with async clients, typed models, cancellation support, and Microsoft.Extensions.AI tools.
  actions:
    - theme: brand
      text: Start building
      link: /guide/quickstart
    - theme: alt
      text: Explore capabilities
      link: /guide/capabilities
features:
  - icon: "01"
    title: One authenticated client
    details: Resolve API keys from constructor values, environment variables, or local .env files.
  - icon: "02"
    title: Full discovery workflow
    details: Search, extract, crawl, map, submit research, and poll results through async methods.
  - icon: "03"
    title: Ready for agents
    details: Expose search and extraction as Microsoft.Extensions.AI AIFunction tools.
---

<div class="home-note">
  <strong>Package:</strong> `Tavily` targets .NET 10, .NET Framework 4.7.2, and .NET Standard 2.0.
</div>

## Choose your next step

<div class="home-paths">
  <a href="/guide/quickstart" class="home-path">
    <strong>Make your first request</strong>
    <span>Install the package, resolve a key, and run a typed search.</span>
  </a>
  <a href="/guide/authentication" class="home-path">
    <strong>Configure authentication</strong>
    <span>Use explicit keys, environment variables, or local development files.</span>
  </a>
  <a href="/reference/models" class="home-path">
    <strong>Find an operation</strong>
    <span>Map Tavily endpoints to client methods and request models.</span>
  </a>
</div>

## Built for application code

The SDK keeps Tavily operations close to ordinary .NET code: inject an
`HttpClient`, pass strongly typed request objects, await the response, and use
the same `CancellationToken` through your application workflow.

<div class="home-grid">
  <a href="/guide/capabilities" class="home-grid-item">
    <span class="home-grid-kicker">DISCOVER</span>
    <strong>Search and retrieve</strong>
    <span>Search the web, extract pages, crawl sites, and map linked content.</span>
  </a>
  <a href="/guide/ai-tools" class="home-grid-item">
    <span class="home-grid-kicker">AGENTS</span>
    <strong>Expose tools</strong>
    <span>Wrap search and extraction for Microsoft.Extensions.AI tool calling.</span>
  </a>
  <a href="/guide/http-client" class="home-grid-item">
    <span class="home-grid-kicker">CONTROL</span>
    <strong>Own the transport</strong>
    <span>Configure timeouts, handlers, proxies, and custom API base addresses.</span>
  </a>
</div>
