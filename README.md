# hossain.dev
Personal developer site with .dev domain. [Preview Site](https://hossain.dev/)

> TIP: To setup custom domain with GitHub pages, see guideline at https://link.medium.com/GtiJJVEV83 

### Local Development
Run following to validate html page.
```shell script
npx html-validate index.html
```


## Tip
Use following to run local server for development from macOS.
```shell
python -m SimpleHTTPServer 8000

# On new MacOS with Python 3
python3 -m http.server

Then visit: http://localhost:8000/
```

### Run locally from *NIX

Alternative universal way to run it from Windows, MacOS or Linux using npm module.

```shell
npm install --global http-server
http-server ./ -a 127.0.0.1 --port 80 --cors
```

## Service Worker & Cache Versioning

The site uses a simple service worker (`sw.js`) to precache static assets for offline support.

### Cache Version Bump (Current: `v2`)

- The constant `CACHE_VERSION` inside `sw.js` was bumped to `v2` to force clients with an older cache to download the latest assets.
- Changing the version automatically:
	1. Creates a new cache bucket named `hossain-dev-cache-<version>`.
	2. Triggers the `install` event to re-prefetch core assets.
	3. On `activate`, old cache buckets are purged.
	4. `skipWaiting()` + `clients.claim()` ensure the new service worker takes control ASAP.

### When to bump
Increment `CACHE_VERSION` when you:
- Remove or rename existing static files.
- Make breaking changes to bundled CSS/JS/HTML where stale assets could cause layout or functional issues.

Not always needed when you only add new assets (they’ll be fetched normally), but bumping is a safe way to guarantee freshness.

### How to bump
Edit at the top of `sw.js`:
```js
const CACHE_VERSION = 'v3';
```
Deploy the change; visitors will transparently update on next load.

### Debugging
- In Chrome DevTools > Application > Service Workers: check the active worker and cache storage entries.
- Use “Update” or “Unregister” to simulate a first visit.
- Delete specific caches under Application > Storage > Cache Storage if testing version transitions.

### Gotchas
- If you rely on aggressive CDN caching for `sw.js`, ensure its HTTP response headers allow timely revalidation (`Cache-Control: no-cache` or a short `max-age`).
- Avoid extremely frequent version bumps to reduce redundant bandwidth usage for returning users.

