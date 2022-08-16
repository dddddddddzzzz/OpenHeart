# Open Heart Protocol

The Open Heart protocol lets an anonymous user sends an emoji reaction to a URL.

## How

Set up an endpoint to receive an Open Heart `POST` request like this one:

```
curl -d '🫠'  -X POST '<url>'
```

A Open Heart message should contain of a single emoji sequence. However, the emoji sequence may be followed by arbitrary data which the server is expected to ignore. 

This allows HTML `<form>`s to post reactions using the Open Heart protocol through an empty input. In this case, the payload will be `🫠=`.
## Server code examples

- [With Cloudflare Worker & Cloudflare KV](https://gist.github.com/muan/388430d0ed03c55662e72bb98ff28f03)
- [With Glitch and `fasify`](https://glitch.com/edit/#!/open-heart-server-demo)

## UI

It's a good idea to give visitors an easy way to send such requests; for example, with:

- [`<open-heart>`](https://github.com/mochokidae/open-heart-element)

## Count

Optionally, a `GET` request to the same URL may respond with the emoji reaction counts.

The response should be a JSON object mapping Emoji (as Strings) to their count (as Strings):

```json
{"❤️":"1","🫀":"2","❤️‍🔥":"3"}
```

If reaction counts are read-only, the server should respond with a 404.

## Real life implementations

- [https://muan.co](https://muan.co/pages/open-heart#like-prompt)

## Questions

### Why not [`WebMention`](https://webmention.rocks/)?

This is simpler.

### What happens after POST?

The author of the endpoint decides.

### What if the someone repeatedly sends emoji to my server?

It shows they may be quite enthusiastic.

### What if I don't want to receive some emoji?

Create a server-side allow list or disallow list and respond with a [400](https://http.cat/400).
