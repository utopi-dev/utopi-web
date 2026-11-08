# utopi-web Specification

**Version**: 0.1 (draft)
**Date**: 2026-11-08
**Status**: Initial draft

## Overview

utopi-web is the public-facing website for **utopi.dev**. It is a Go application designed for modern web standards only.

### Goals

- Serve the utopi.dev public website
- Enforce modern security standards (TLS 1.3 only)
- Provide a fast, simple, maintainable codebase
- Use htmx for dynamic interactions without a full SPA framework
- Generate type-safe HTML with templ

### Non-Goals

- Support for legacy browsers (IE, old Safari, etc.)
- Support for TLS < 1.3
- Client-side JavaScript frameworks (React, Vue, etc.)
- External HTTP frameworks (Gin, Echo, Fiber, etc.)

## Company Projects

The projects associated with utopi.dev are documented in [project-list.md](./project-list.md) (bilingual: French on top, English below).

## Technology Stack

| Component     | Choice                  | Rationale                                      |
|---------------|-------------------------|------------------------------------------------|
| Language      | Go (latest stable)      | Performance, simplicity, strong stdlib         |
| HTTP Server   | `net/http`              | Native, no external dependencies               |
| TLS           | Custom `crypto/tls`     | Enforce TLS 1.3 minimum                        |
| Templating    | templ                   | Type-safe, compile-time HTML generation        |
| Frontend      | htmx                    | Progressive enhancement, minimal JS            |
| Static Assets | Embedded via `embed`    | Single binary deployment                      |

## TLS Requirements

- **Minimum version**: TLS 1.3 (`tls.VersionTLS13`)
- **Cipher suites**: Go defaults for TLS 1.3 only
- **Certificates**: ACME (Let's Encrypt) or manual; exact method TBD
- **HTTP/2**: Enabled (default with TLS 1.3 in Go)
- **Legacy protocols**: Explicitly disabled (TLS 1.0, 1.1, 1.2 rejected)

The server must refuse connections that do not negotiate TLS 1.3.

## Browser Compatibility

Supported:
- Latest two versions of Chrome, Firefox, Safari, Edge
- Modern mobile browsers with TLS 1.3 support

Not supported:
- Any browser that does not support TLS 1.3
- Internet Explorer
- Legacy mobile browsers

No polyfills or fallbacks will be provided.

## Architecture Principles

1. **Single binary**: All assets and templates embedded where practical
2. **Minimal dependencies**: Prefer stdlib; only add templ + htmx
3. **Server-rendered**: HTML generated on the server with templ
4. **htmx-driven interactivity**: Partial page updates via htmx attributes
5. **Security by default**: Strict TLS, secure headers, no unnecessary exposure

## Directory Structure (planned)

```
.
├── cmd/
│   └── server/          # main entrypoint
├── internal/
│   ├── handlers/        # HTTP handlers
│   ├── templates/       # templ source files
│   └── assets/          # static files
├── docs/
├── go.mod
├── README.md
├── SPEC.md
└── project-list.md
```

## Open Questions

- Exact TLS certificate management strategy
- Deployment target (VPS, container, serverless?)
- Content management approach (static files vs. simple CMS)
- Analytics / monitoring requirements

## Next Steps

1. Initialize Go module
2. Add basic server with TLS 1.3 enforcement
3. Integrate templ
4. Create initial page templates
5. Add htmx
