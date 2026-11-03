# Cowork Plugin Builder

Build Microsoft Copilot Cowork plugin packages through a guided browser-based wizard.

Cowork Plugin Builder helps authors create, validate, and export Microsoft 365 app packages for Copilot Cowork without manually assembling every manifest and ZIP entry.

## Live Builder

Use the live app here: https://victorious-smoke-012ce9c1e.7.azurestaticapps.net/

## What This Is

Cowork Plugin Builder is an authoring and validation tool. It generates a ZIP containing a v1.29 manifest, required icons, and optional skills. Connectors are configured using their HTTPS endpoint, metadata, and authentication; static tool-definition authoring is not required.

The package validator checks manifest fields, skill frontmatter, archive structure, companion-file limits, connector configuration, exact MCP file paths, tool schemas, and safety annotations.

## Who It Is For

- Plugin authors and maintainers
- Internal platform teams preparing plugin packages
- Developers validating plugin structure before publishing

## How To Use

1. Open the live builder link.
2. Complete each wizard step in order.
3. Add identity, mode, skills, and one or more connectors.
4. Review preview and validation output.
5. Export the generated package.
6. Sideload or publish the ZIP through your supported Microsoft 365 workflow.

For MCP connectors, supply a real HTTPS endpoint and the authentication settings required by that server. Cowork discovers tools dynamically through `tools/list`. The builder does not include a tool-definition editor or emit tool-description files.

Cowork discovers and invokes tools on the live server. Packaged tool definitions do not create tools or change runtime confirmations. A package that passes static validation still needs a successful installation, authentication, and live tool-call test.

## Current Support

- Microsoft 365 Unified App Manifest v1.29
- Official bundled schema validation, generated-file checks, and icon dimension checks
- Editable app ID and version for maintaining existing plugins
- Skills-only, connector-only, and skills-plus-connector packages
- Agent Skills using `skills/<name>/SKILL.md`
- Remote HTTPS MCP connectors
- URL-based MCP configuration with live server tool discovery
- Anonymous (`None`), OAuth (`OAuthPluginVault`), and Cowork-only Dynamic Client Registration authentication
- Claude Code, Cursor, and open-plugin import with optional skill frontmatter and companion files preserved, `.mcp.json` / `mcp.json` support, and up to 10 HTTPS MCP servers imported
- Browser-side ZIP generation and package validation

## Current Limits

- Up to 20 skills per package
- Up to 10 connectors per package
- Skill names: 1-64 characters in kebab-case
- Skill descriptions: 1-1,024 characters
- Up to 20 companion files per skill
- Companion files: 5 MB each and 10 MB total per skill
- MCP server URLs must use HTTPS

API-key authentication is present in the manifest schema but isn't currently supported by Cowork. Use `None`, `OAuthPluginVault`, or Dynamic Client Registration in the builder.

Manifest v1.29 permits an optional `mcpToolDescription`. The ZIP validator checks supplied descriptions, including relative references such as `./mcp-tools.json`, without exposing an authoring editor. Legacy v1.28 uploads receive a clear upgrade message.

Keep the app ID stable across updates and increment the app version. Review conversions in the wizard before exporting; unsupported source features and authentication assumptions are reported rather than silently treated as working.

For workspace file inputs, the server's tool schemas should use `contentEncoding: base64`; Cowork handles encoding outside the model context. Use at most one array file input per tool.

The builder does not run Microsoft's App Validation Library. For a wiqd project, run `wiqd plugin validate --mode deep`, then sideload and exercise the real connector. Custom plugins are not supported on Cowork mobile, and tenant governance can block upload or installation.

## Documentation

- [Step-by-step: Build a DeepWiki-powered Cowork plugin](https://suvidhablogpost.wordpress.com/2026/09/22/build-a-deepwiki-powered-cowork-plugin/) — create a Cowork plugin that combines the DeepWiki Public MCP server with a custom skill.
- [Build plugins for Copilot Cowork](https://learn.microsoft.com/en-us/copilot/cowork/cowork-plugin-development)
- [Register MCP servers as agent connectors](https://learn.microsoft.com/en-us/microsoftteams/platform/m365-apps/agent-connectors)
- [Microsoft 365 Agents Toolkit CLI](https://learn.microsoft.com/en-us/microsoftteams/platform/toolkit/microsoft-365-agents-toolkit-cli)
- [Configure authentication for MCP and API plugins](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/plugin-authentication)

## Security And Privacy

- This repository contains only public documentation.
- The underlying source code is maintained in a private repository.
- The live app sends cookie-free operational telemetry for page views, package exports, converter use, and validator use. Events do not include plugin content, text fields, MCP URLs, or URL query strings.
- Do not upload secrets in plugin text fields.
- Connector credentials aren't placed in generated manifests or skill files.

## Status

This project is actively maintained. Documentation alignment was checked on November 3, 2026. The package target is Microsoft 365 Unified App Manifest v1.29.
