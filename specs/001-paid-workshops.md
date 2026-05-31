# Paid Workshops on Open Learn

**Status:** Concept · v1 · for discussion
**Scope:** Architecture only · no implementation

## Problem

Workshop creators want to monetize their content. Open Learn is a static web app without backend and should stay that way. The challenge: enable paid workshops without giving up the static architecture, without adding accounts, and without making the platform process payments.

## Architectural Principle: Two-System Split

Open Learn and the sales process are two separate systems, connected only by URLs.

```
┌─────────────────────────────────────────────┐
│ Workshop Landing Page                       │
│ (one per workshop, hosted by creator)       │
│                                             │
│ - Static HTML + payment widget              │
│ - Backend allowed (Cloudflare Worker, etc.) │
│ - Verifies purchase, issues unlock link     │
└─────────────────────────────────────────────┘
                    │
                    │  URL with secret path or token
                    ▼
┌─────────────────────────────────────────────┐
│ Open Learn                                  │
│ (single static app, hosted by us)           │
│                                             │
│ - No backend, no accounts                   │
│ - Fetches YAML from given URL               │
│ - Renders content                           │
│ - Never sees money or customer identity     │
└─────────────────────────────────────────────┘
```

The landing page handles the entire commercial transaction. Open Learn handles only the learning experience.

## Learner Flow

A customer named Anna discovers a workshop. Her journey:

1. **Discovery.** Anna lands on the workshop's landing page (search, social, ad).
2. **Free preview.** She clicks "Start free preview". This opens Open Learn with a public YAML URL that contains only the preview lessons.
3. **Decision.** Anna decides she wants the full course. She returns to the landing page.
4. **Purchase.** She pays on the landing page (Stripe, PayPal, whatever the creator wires up). Open Learn is not involved at this step.
5. **Unlock link.** The landing page backend verifies the payment and emails Anna a unique link with an unguessable path or token.
6. **Full access.** Anna clicks the link. It opens Open Learn with a different YAML URL that contains all lessons. Open Learn renders the full workshop without knowing why it has access.

## Creator Setup

What the workshop creator does once:

1. Build the workshop content (YAML, images, audio, videos) as a normal workshop.
2. Host two YAML entry points on a static host (GitHub Pages, S3, IPFS, anywhere):
   - **Public entry:** `index.yaml` listing only preview lessons.
   - **Private entry:** `unlock-<secret>/index.yaml` listing all lessons. The secret is long, random, and unguessable.
3. Set up a landing page using the landing-page library (existing today as `index.html` per workshop repo).
4. Wire the landing page to a payment provider and a small backend (serverless function) that:
   - Receives webhook on successful payment.
   - Generates a fresh unlock path or token per customer.
   - Emails the customer their unlock link.

The creator owns the payment relationship, the backend, the costs, and the customer data. Open Learn is the renderer.

## The Hard Question: Access Verification Without a Backend in Open Learn

Open Learn must not gain a backend. So how does the platform "know" that a particular learner has access to paid lessons? Three options, each with trade-offs:

### Option A — Unguessable URL Path (path-as-secret)

The paid lessons live under a long random folder name in the creator's hosting:

- Public: `creator.github.io/workshop/index.yaml`
- Per customer: `creator.github.io/workshop/unlock-a8f3b2c1d4e5/index.yaml`

After payment, the backend generates a unique secret, copies the full workshop into that folder (or symlinks), and sends Anna the URL. Anyone with that URL can access the lessons — but only Anna received it.

**Pros:** Zero changes in Open Learn. Pure static hosting. No keys, no JWT, no crypto in the browser.
**Cons:** Anna can share her link. No revocation. No per-customer expiry without rotating URLs.

### Option B — Signed Tokens (JWT)

The backend signs a JSON Web Token containing customer ID, workshop ID, and expiry. The unlock URL contains the token. Open Learn reads the token, verifies the signature against the creator's public key (fetched once), and unlocks paid sections.

**Pros:** Revocation possible (publish a blocklist). Time-limited access. One signing key per creator.
**Cons:** Requires Open Learn to gain JWT logic. The paid YAML must still be served somewhere — typically gated behind the same token-checking endpoint, which means the creator needs a serving backend anyway.

### Option C — Encrypted Payload

The paid YAML is encrypted with a workshop-wide key. The unlock URL contains the key. Open Learn decrypts in the browser.

**Pros:** The encrypted file can sit on any public host. Only customers with the key see content.
**Cons:** Same key for everyone — one customer leaks the key and everyone has access. Open Learn needs crypto logic.

### Recommendation Pattern (for discussion)

Start with **Option A** for the MVP: it requires zero changes in Open Learn and zero browser crypto. Sharing is a real risk, but for an MVP we accept it. Migrate to Option B if leakage becomes a measurable problem and revocation becomes worth the complexity.

## What Open Learn Needs (Minimal UI)

1. **Lock indicator** in the lessons grid: a small icon on lessons the current YAML source does not include.
2. **"Upgrade" callout** on locked lessons: when the user clicks a locked lesson, show a card linking back to the workshop's landing page.

That is the entire Open Learn footprint. No accounts, no payment, no backend. The lock icon is purely cosmetic — the actual gating is whether the YAML source lists the lesson at all.

## What the Landing Page Library Needs

Today the library renders `README.md` + `CHANGELOG.md` for each workshop. Additions:

1. **Pricing block** in `workshop.config.yaml`: price, currency, payment provider key.
2. **Preview/Paid lesson list** with lock icons.
3. **Checkout flow** (provider-agnostic — Stripe, Lemon Squeezy, Gumroad).
4. **Webhook receiver** (serverless function: Cloudflare Workers, Vercel Functions, Netlify Functions).
5. **Unlock link generator + email sender.**

All of this lives in the workshop creator's deployment, not in Open Learn.

## Business Model

Open Learn is not a passive player. The creator supplies only raw content (YAML, videos);
Open Learn turns it into the sellable product — a story-mode course with a learning path,
quizzes, audio, progress and sync. That transformation is the value.

From this follows how Open Learn earns:

- The creator **offers the course through Open Learn** — presented in the Open Learn experience.
- **Selling happens on a separate page** (payment is never inside the learning plugin).
- **Selling is a feature** the Open Learn ecosystem provides — and for that, **Open Learn can
  take a share of each sale.**

Open Learn earns not by handling money, but by providing the presentation that makes a course
sellable and by enabling the sale as a feature. Concrete revenue mechanics (share size,
who collects, payout) are an open question.

## What This Concept Does Not Do

- No payment logic inside Open Learn (the learning plugin stays static, no backend).
- No accounts or user identity in Open Learn.
- No DRM. Sharing is technically possible under Option A.
- No platform-wide marketplace. Discovery stays mostly the creator's job (a curated
  "featured" list is an open question — see below).

## Open Questions

1. Option A vs B vs C for the MVP — which fits the values of the platform best?
2. Should the landing page library live in the `openlearnapp` org or as a separate template repo creators clone?
3. Which payment provider do we ship as the reference integration?
4. How do we handle refunds? Manual via the creator, or automated revocation?
5. Should the unlock link expire? If yes, after how long?
6. Should Open Learn show a "powered by" or "paid workshop" badge when rendering an unlocked workshop, or stay fully neutral?

## Next Steps

1. Review of this spec.
2. Iterate on the open questions (expected 2-3 rounds).
3. Once aligned: move into `plans/` with a concrete build plan for the landing page library extension.
4. Implementation only after explicit go-ahead.
