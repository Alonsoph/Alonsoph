Alonso Pinto

First-year student of Fundamental Informatics and Information Technologies (02.03.02) at Southern Federal University. Based in Chile.

I build and operate web products that have real users and paying customers. Everything linked below is live in production — not a course project, not a mockup.

What I run
TuWebIglesia — multi-tenant SaaS

A platform that generates and hosts websites for evangelical churches in Chile. Each church gets its own site on a subdomain or its own domain, and its pastor edits the content through a self-service panel — no developer in the loop.

Node.js / Express API on Railway · PostgreSQL · React + Vite on Vercel · Cloudinary for media · Flow for payments

Subscription product with tiered plans. A navigable demo is embedded on the landing page.

Frontis — custom sites for small businesses

Six client sites currently in production, across industries that have nothing in common: pressed-flower art, custom furniture, private security, heavy machinery transport, education, and lodging. Each one is built from the client's own photos, brand, and words.

Bloom · El Creador · Icalma · C&C Transporte · Comunidad Conexión · Las Piedras del Río Bueno

Engineering notes

A few decisions from TuWebIglesia that I can walk through in detail:

Tenant isolation comes from the token, never the request. Every panel query derives the church ID from the verified JWT claims, not from a URL parameter or request body — so a pastor cannot reach another church's content by editing a number in the request.
Every database query is parameterized. No string interpolation of user input into SQL, anywhere in the codebase.
The payment webhook doesn't trust its own callback. When the provider posts a confirmation, the API takes the token, re-queries the provider's API over an HMAC-signed request, and only then writes the result. A forged callback buys nothing.
One connection pool with explicit limits, shared across the app — max connections, idle timeout, and connection timeout set deliberately rather than left to defaults.
Thirteen site templates share a single presentation layer. The templates don't share CSS class names, so the shared motion and accessibility layer anchors structurally instead of by class, and ships behind an environment-variable kill switch for staged rollout and instant rollback.
Rendered pages are cached with explicit invalidation on every content edit, so a pastor's change appears immediately without serving stale HTML to visitors.

I work with AI coding assistants as a core part of my workflow — it's how one person ships and maintains this much. The architecture decisions, the production incidents, and the bugs are mine.

Languages

Spanish (native) · English (fluent) · Russian (basic)

Contact

higinio.pinto.h@gmail.com
