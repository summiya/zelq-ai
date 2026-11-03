# ZELQ AI

A lightweight, responsive showcase for NEXUS, Spurel, and Atlas.

## Design

The approved original dark-mode website design is preserved. The ZELQ AI logo is the selected cyan-and-purple circuit-inspired mark **without** the “AI ENGINEERING PORTFOLIO” subtitle.

- Animated hero artwork and interactive project cards
- Project-category filters, accent switcher, mobile navigation
- No build tools, dependencies, database, cookies, tracking, or external API requests
- The entire site, including logo and favicon, is in `index.html`

## Preview locally

Clone the repository and open `index.html` in a browser, or serve it:

```bash
python3 -m http.server 4173
```

Then open `http://localhost:4173`.

## Oracle Always Free hosting

This site is static. Serve `index.html` with Nginx on the existing Oracle VPS; no persistent Node.js server is needed.

1. Point the domain's DNS A record to the Oracle VPS public IP.
2. Configure Nginx to serve the website from its deployment directory.
3. Configure HTTPS using Let's Encrypt / Certbot, and keep ports 80/443 permitted at the cloud and OS firewalls.
4. For updates, pull the newest `main` branch into the server's site directory.

The site has **not been deployed to Oracle** as part of this GitHub publication.

## Project status

- **NEXUS:** AI workspace; in development — [source](https://github.com/summiya/nexus)
- **SPUREL:** RAG retrieval observability workbench; pre-alpha — [source](https://github.com/summiya/spurel)
- **ATLAS:** Distributed ingestion and search platform; architecture and planning only — [source](https://github.com/summiya/Atlas)

Project descriptions and statuses should be checked against the project repositories before public launch.
