# ZELQ AI

A fast, static interactive showcase for NEXUS, Spurel (RAG retrieval), and Atlas.

## Interactive demos

- **NEXUS** — sample workflow exploration for knowledge, tools and model routing
- **Spurel** — sample retrieval rankings, document chunks and retrieval modes
- **Atlas** — animated sample ingestion and indexing pipeline
- Scroll reveals, ambient animation, project cards and responsive mobile layout

All demos use **synthetic example data** and are not connected to production backends. Atlas is in planning; Spurel is pre-alpha; NEXUS is actively being developed.

## Run locally

Open `index.html` in a browser, or:

```bash
python3 -m http.server 4173
```

Then visit http://localhost:4173.

## Oracle VPS deployment

See the [Oracle deployment guide](deploy/README.md) and [Nginx server configuration](deploy/nginx-zelq-ai.conf).

The site is a single self-contained HTML file, so **no Node.js process, database, or build step** is required. Nginx serves the home page at `/` (without a visible `.html` extension) and applies gzip compression for efficient delivery.

**Minification is not a security boundary:** client-side code remains inspectable in the browser and this repository is public. Do not put private tokens, API secrets, or sensitive business logic into the site.

**Source repositories:** [NEXUS](https://github.com/summiya/nexus), [Spurel](https://github.com/summiya/spurel), [Atlas](https://github.com/summiya/Atlas).
