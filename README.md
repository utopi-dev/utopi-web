# utopi-web

Public website for [utopi.dev](https://utopi.dev).

## Stack

- **Language**: Go (latest stable)
- **HTTP**: Native `net/http` (no external frameworks)
- **Templating**: [templ](https://templ.guide/)
- **Interactivity**: [htmx](https://htmx.org/)
- **TLS**: Custom TLS configuration enforcing **TLS 1.3 only**
- **Browser support**: Modern browsers only (no legacy polyfills or fallbacks)

## Design Principles

- Minimal dependencies
- Security-first: latest TLS exclusively
- Progressive enhancement via htmx
- Type-safe HTML with templ
- Intentionally incompatible with older browsers and TLS versions

## Documentation

- [SPEC.md](./SPEC.md) — Technical specification and requirements
- [docs/ARCHITECTURE.md](./docs/ARCHITECTURE.md) — System architecture (coming soon)
- [project-list.md](./project-list.md) — Company projects (French on top, English below)

## Getting Started

```bash
git clone https://github.com/utopi-dev/utopi-web.git
cd utopi-web
go mod tidy
# templ generate (after adding templates)
go run .
```

## License

TBD
