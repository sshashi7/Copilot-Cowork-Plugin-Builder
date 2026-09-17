# Cowork Plugin Builder

Build Microsoft Copilot Cowork plugin packages through a guided browser-based wizard.

Cowork Plugin Builder helps authors create, validate, and export Microsoft 365 app packages for Copilot Cowork without manually assembling every manifest and ZIP entry.

## Live Builder

Use the live app here: https://victorious-smoke-012ce9c1e.7.azurestaticapps.net/

## What This Is

Cowork Plugin Builder is an authoring and validation tool. It generates a ZIP containing the v1.28 manifest, required icons, skills, and connector tool descriptions at the package root.

The package validator checks manifest fields, skill frontmatter, archive structure, companion-file limits, connector configuration, exact MCP file paths, tool schemas, and safety annotations.

## Who It Is For

- Plugin authors and maintainers
- Internal platform teams preparing plugin packages
- Developers validating plugin structure before publishing

## How To Use

1. Open the live builder link.
2. Complete each wizard step in order.
3. Add identity, mode, skills, and connector details.
4. Review preview and validation output.
5. Export the generated package.
6. Sideload or publish the ZIP through your supported Microsoft 365 workflow.

For MCP connectors, define tools in the visual builder, import an MCP `tools/list` response, or apply raw tool-description JSON. Every option populates the same visual tool details for review and generates the root-level `mcp-tools.json` referenced by the manifest. Tool names, parameters, schemas, and safety annotations must match the tools exposed by the server.

## Current Support

- Microsoft 365 Unified App Manifest v1.28
- Skills-only, connector-only, and skills-plus-connector packages
- Agent Skills using `skills/<name>/SKILL.md`
- Remote HTTPS MCP connectors
- Visual MCP tool authoring, `tools/list` import, and raw JSON editing
- Anonymous (`None`) and OAuth (`OAuthPluginVault`) connector authentication
- Claude Code, Cursor, and open-plugin import with skill companion files preserved
- Browser-side ZIP generation and package validation

## Current Limits

- Up to 20 skills per package
- Up to 10 connectors per package
- Skill names: 1-64 characters in kebab-case
- Skill descriptions: 1-1,024 characters
- Up to 20 companion files per skill
- Companion files: 5 MB each and 10 MB total per skill
- MCP server URLs must use HTTPS

API-key authentication is present in the v1.28 manifest schema but isn't currently supported by Cowork. Use `None` or `OAuthPluginVault` in the builder.

## Documentation

- [Build plugins for Copilot Cowork](https://learn.microsoft.com/en-us/microsoft-365/copilot/cowork/cowork-plugin-development)
- [Microsoft 365 Agents Toolkit CLI](https://learn.microsoft.com/en-us/microsoftteams/platform/toolkit/microsoft-365-agents-toolkit-cli)
- [Configure authentication for MCP and API plugins](https://learn.microsoft.com/en-us/microsoft-365/copilot/extensibility/plugin-authentication)

## Security And Privacy

- This repository contains only public documentation.
- The underlying source code is maintained in a private repository.
- The live app sends cookie-free operational telemetry for page views, package exports, converter use, and validator use. Events do not include plugin content, text fields, MCP URLs, or URL query strings.
- Do not upload secrets in plugin text fields.
- Connector credentials aren't placed in generated manifests or skill files.

## Status

This project is actively maintained. The current package target is Microsoft 365 Unified App Manifest v1.28.
