# ZELQ AI — Interactive Project Showcase

A lightweight, responsive static website featuring **NEXUS**, **Spurel** and **Atlas**, retaining the approved ZELQ AI logo and homepage design.

## What's in V2

- NEXUS: interactive simulated AI workflow and prompt explorer
- Spurel: simulated retrieval inspector with vector, keyword and hybrid ranking modes, Top K, and document chunk details
- Atlas: animated document ingestion pipeline simulator with run, pause and reset
- Scroll-triggered reveals, ambient animations, reading progress indicator and sticky navigation
- Project card detail views and links to each interactive demo
- Responsive desktop and mobile layout, plus reduced-motion support

**Important:** The experiences are **illustrative concept demos with synthetic sample data**, not production screenshots or connected backend tools. They make no live requests to AI, databases, search services or document stores. Atlas is in planning; Spurel is pre-alpha; NEXUS is in active development.

## Run locally

Everything needed is embedded in `index.html` (CSS, JavaScript, selected ZELQ AI logo, favicon).

```bash
python3 -m http.server 4173
```

Open http://localhost:4173 in your browser. Alternatively, double-click `index.html` to view directly.

## Deploy to Oracle Always Free VPS

Serve `index.html` with Nginx from your existing Oracle VM. The site needs **no Node.js process**, database, paid services or API keys.

1. Clone or pull this repo on the server and copy `index.html` to your Nginx website root.
2. Point the domain's DNS A record to the VM public IP.
3. Configure Nginx to serve the page and allow ports 80 and 443 in the Oracle security rules and VM firewall.
4. Use Certbot/Let's Encrypt for HTTPS.

Publishing to GitHub does not deploy the site on the Oracle VPS.

## Source projects

- [NEXUS](https://github.com/summiya/nexus) — AI workspace
- [Spurel](https://github.com/summiya/spurel) — RAG retrieval observability and evaluation workbench
- [Atlas](https://github.com/summiya/Atlas) — planned distributed ingestion and search system

The demo dashboards are **not** screenshots of these projects and their sample metrics are not genuine performance claims.
