---
layout: default
---
# Open Heart Protocol

Open Heart Protocol lets an anonymous user sends an emoji reaction to a URL.

<div class="reactions">
<open-heart href="https://api.openheart.fyi" emoji="❤️">❤️</open-heart>
<open-heart href="https://api.openheart.fyi" emoji="🫀">🫀</open-heart>
<open-heart href="https://api.openheart.fyi" emoji="🥨">🥨</open-heart>
</div>

## How

Set up an endpoint to receive an Open Heart POST request like this one:

```
curl -d '🫠'  -X POST '<url>'
```


## Server code examples

- [With Cloudflare Worker & Cloudflare KV](https://gist.github.com/muan/388430d0ed03c55662e72bb98ff28f03)
- [With Glitch and `fasify`](https://glitch.com/edit/#!/open-heart-server-demo)

## UI

It's a good idea to give visitors an easy way to send such requests; for example, with:

- [`<open-heart>`](https://github.com/mochokidae/open-heart-element)

## Count

Optionally, a GET request to the same URL could respond with the emoji reaction counts.

## Real life implementations

- https://api.openheart.fyi (Allow listed emoji include ❤️, 🫀, and 🥨)

  `curl -d '🥨' -X POST 'https://api.openheart.fyi'`

  `curl 'https://api.openheart.fyi'`

## Questions

### Why not [`WebMention`](https://webmention.rocks/)?

This is simpler.

### What happens after POST?

The author of the endpoint decides.

### What if the someone repeatedly sends emoji to my server?

It shows they may be quite enthusiastic.

### What if I don't want to receive some emoji?

Create a server-side allow list or disallow list and respond with a [400](https://http.cat/400).
