# Open Heart Protocol

The Open Heart protocol lets an anonymous user sends an emoji reaction to a URL.

## How

Set up an endpoint to receive an Open Heart `POST` request like this one:

```bash
curl -d '🥨' -X POST 'https://api.oh.dddddddddzzzz.org/github.com/dddddddddzzzz/OpenHeart'
```

A Open Heart message should contain of a single emoji sequence. However, the emoji sequence may be followed by arbitrary data which the server is expected to ignore. 

This allows HTML `<form>`s to post reactions using the Open Heart protocol through an empty input. In this case, the payload will be `🥨=`.

---

Optionally, a `GET` request to the same URL may respond with the emoji reaction counts.

```bash
curl 'https://api.oh.dddddddddzzzz.org/github.com/dddddddddzzzz/OpenHeart'
```

The response should be a JSON object mapping Emoji (as Strings) to their count (as Numbers):

```json
{"❤️": 14,"🫀": 12,"🥨": 22}
```

If reaction counts are write-only, the server should respond with a [403](https://http.cat/403) or a [404](https://http.cat/404).

## Usage

In its simplest form, you can put this on your website:
```html
<form action="<your server endpoint>" method="POST" enctype="text/plain">
  <button name="🥨">🥨</button>
</form>
```

However, we have also created [`<open-heart>`](https://github.com/dddddddddzzzz/open-heart-element) for a better user experience.

## Server code

To get started quickly, you can use our [public OpenHeart API](https://github.com/dddddddddzzzz/api-oh?tab=readme-ov-file#put-it-on-your-website-right-now), but we do recommend owning your own data whenever possible.

Here are some code example get your own endpoint running quickly:

- [With Cloudflare Worker & Cloudflare KV](https://gist.github.com/muan/388430d0ed03c55662e72bb98ff28f03)
- [With Glitch and `fasify`](https://glitch.com/edit/#!/open-heart-server-demo)

We welcome examples using other languages and services. Please send us a pull request!

## Questions

### Why not [`WebMention`](https://www.w3.org/TR/webmention/#sending-webmentions)?

This is much, much, much simpler.

### What happens after POST?

The author of the endpoint decides.

### What if the someone repeatedly sends emoji to my server?

It shows they may be quite enthusiastic. 

In all seriousness, our [public API](https://github.com/dddddddddzzzz/api-oh) is built on [Cloudflare Worker](https://workers.cloudflare.com) which comes with rate limiting and DDoS protection.

### What if I don't want to receive some emoji?

Create a server-side allow list or disallow list and respond with a [400](https://http.cat/400).
