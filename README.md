**Cookie Choice** is an endpoint that serves a JS library for rendering a cookie consent banner. Endpoint is a Cloudflare Worker to consider the geolocation.

## Demo

- Live demo: https://pioug.github.io/cookie-choice/example.html
- "Noop" function if not in Europe: https://cookie-choice.pioug.workers.dev/cookie-choice.js?privacy-policy-link=https://github.com/pioug/cookie-choice
- Function to render the banner: https://cookie-choice.pioug.workers.dev/cookie-choice.js?privacy-policy-link=https://github.com/pioug/cookie-choice&force=true

## Why?

- Low latency thanks to Cloudflare CDN
- Visitor's location provided by Cloudflare (neither IP geolocation service nor browser geolocation API are needed)
- Library served only when cookie consent law applies to visitor's country
- Small overhead when cookie consent is not required

## Installation

1. Build the library:

```bash
npm ci
npx rollup -c
```

2. Deploy `cloudflare-worker.js` to Cloudflare Workers.

## Usage

```js
const privacyPolicyLink = "https://my.privacy.policy/";
const force = true;
const {
  renderCookieChoice
} = await import(`https://my.cloudflare.worker/cookie-choice.js?privacy-policy-link=${privacyPolicyLink}&force=${force}`);
renderCookieChoice();
document.body.addEventListener(
  "cookieChoice:accept",
  {
    once: true
  },
  () => {
    console.log("Thanks for the cookies!");
  }
);
```

## Documentation

- https://developers.cloudflare.com/workers/
- https://blog.cloudflare.com/delivering-a-serverless-api-in-10-minutes-using-workers/
- http://ec.europa.eu/ipg/basics/legal/cookies/index_en.htm
