# cookies

Parse and serialize HTTP cookies for [Ecko](https://ecko.sh) client sessions:
read `Set-Cookie` response headers into a jar, and build the `Cookie` request
header to send them back. Written in Ecko; pure, no capabilities.

## Install

```bash
ecko add https://github.com/ecko-sh/cookies
```

## Usage

```ecko
import cookies

jar = cookies.parse("session=abc; Path=/; HttpOnly; Secure; Max-Age=3600")
# { session: { value: "abc", path: "/", http_only: true, secure: true, max_age: 3600 } }

cookies.header(jar)              # "session=abc"  - the Cookie request header

jar = cookies.merge(jar, sc)     # fold a new Set-Cookie into the session jar
jar = cookies.set(jar, "k", "v") # add a cookie by hand
```

## API

| Function | Description |
|---|---|
| `parse(set_cookie)` | Parse one `Set-Cookie` header string (or a list of them) into a jar `{ name: record }` |
| `header(jar)` | Build the `Cookie` request header, `"a=1; b=2"` (names sorted) |
| `set(jar, name, value)` | Add or replace a cookie, returning a new jar |
| `merge(jar, set_cookie)` | Fold a new `Set-Cookie` into a jar (later values win) — for session accumulation |

A record always carries `value`, plus any attributes present: `path`, `domain`,
`expires`, `max_age` (Int), `same_site`, and the `secure` / `http_only` flags
(default `false`).

## Notes

- A cookie value may contain `=` (kept intact); a non-numeric `Max-Age` is
  ignored rather than fatal.
- `header` sends only name=value pairs — attributes are response-only.

## Testing

```bash
ecko test tests/
```

## License

MIT — see [LICENSE](LICENSE).
