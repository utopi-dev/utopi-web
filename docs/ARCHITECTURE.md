# Architecture

**Status**: Draft

## High-Level Design

```
[Browser] --TLS 1.3--> [Go net/http server]
                              |
                              +-- templ handlers (HTML)
                              +-- htmx endpoints (partials)
                              +-- static assets (embed.FS)
```

## Key Components

### TLS Layer

Custom `tls.Config`:

```go
tlsConfig := &tls.Config{
    MinVersion: tls.VersionTLS13,
    // PreferServerCipherSuites not needed in TLS 1.3
}
```

Server created with `http.Server{TLSConfig: tlsConfig}`.

### Routing

Standard library `http.ServeMux` (Go 1.22+ enhanced patterns).

### Templating

- Source: `*.templ` files
- Generated: `*_templ.go` (checked in or generated in CI)
- Called from handlers: `component.Render(w, data)`

### htmx

- Loaded via CDN or embedded
- Used for:
  - Form submissions
  - Partial content updates
  - Search / filtering
- No custom JavaScript beyond htmx

## Security

- TLS 1.3 only
- Secure headers (HSTS, CSP, etc. — to be defined)
- No mixed content
- Cookie flags: Secure, HttpOnly, SameSite

## Deployment

Single binary. Environment variables for configuration (port, cert paths, etc.).

TBD: reverse proxy vs. direct TLS termination.
