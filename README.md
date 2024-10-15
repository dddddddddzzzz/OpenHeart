# Open Heart Protocol

The Open Heart protocol lets an anonymous user sends an emoji reaction to a URL.

## How

Set up an endpoint to receive an Open Heart `POST` request like this one:

```bash
curl -d '🥨' -X POST 'https://api.openheart.fyi'
```

A Open Heart message should contain of a single emoji sequence. However, the emoji sequence may be followed by arbitrary data which the server is expected to ignore. 

This allows HTML `<form>`s to post reactions using the Open Heart protocol through an empty input. In this case, the payload will be `🥨=`.

```html
<form action="https://api.openheart.fyi" method="POST" enctype="text/plain">
  <button name="🥨">🥨</button>
</form>
```

## Server code

### Example

- [With Cloudflare Worker & Cloudflare KV](https://gist.github.com/muan/388430d0ed03c55662e72bb98ff28f03)
- [With Glitch and `fasify`](https://glitch.com/edit/#!/open-heart-server-demo)

### Public API

Alternatively, you can use the public OpenHeart API provided by us. See the [repository](https://github.com/dddddddddzzzz/api-oh) for more details.

## UI

It's a good idea to give visitors an easy way to send such requests; for example, with:

- [`<open-heart>`](https://github.com/dddddddddzzzz/open-heart-element)

## Count

Optionally, a `GET` request to the same URL may respond with the emoji reaction counts.

```bash
curl 'https://api.openheart.fyi'
```

The response should be a JSON object mapping Emoji (as Strings) to their count (as Numbers):

```json
{"❤️": 14,"🫀": 12,"🥨": 22}
```

If reaction counts are write-only, the server should respond with a [403](https://http.cat/403) or a [404](https://http.cat/404).

## Questions

### Why not [`WebMention`](https://www.w3.org/TR/webmention/#sending-webmentions)?

This is much, much, much simpler.

### What happens after POST?

The author of the endpoint decides.

### What if the someone repeatedly sends emoji to my server?

It shows they may be quite enthusiastic.

### What if I don't want to receive some emoji?

Create a server-side allow list or disallow list and respond with a [400](https://http.cat/400).
