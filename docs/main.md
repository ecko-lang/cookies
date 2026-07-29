# cookies

## `parse(set_cookie)`

parse(set_cookie) -> jar. Accepts one Set-Cookie header string or a list.

## `header(jar)`

header(jar) -> "name=value; ..." for the Cookie request header (names sorted;
attributes are response-only and not sent).

## `set(jar, name, value)`

set(jar, name, value) -> jar with a cookie added or replaced.

## `merge(jar, set_cookie)`

merge(jar, set_cookie) -> jar with cookies from a new Set-Cookie folded in
(later values win) - the session-accumulation helper.
