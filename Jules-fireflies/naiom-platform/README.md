This is a [Next.js](https://nextjs.org) project bootstrapped with [`create-next-app`](https://nextjs.org/docs/app/api-reference/cli/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `app/page.tsx`. The page auto-updates as you edit the file.

This project uses [`next/font`](https://nextjs.org/docs/app/building-your-application/optimizing/fonts) to automatically optimize and load [Geist](https://vercel.com/font), a new font family for Vercel.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js) - your feedback and contributions are welcome!

## Deploy on Render

This repo ships a `render.yaml` Blueprint (at the repo root) that points Render at this
directory (`Jules-fireflies/naiom-platform`), with `npm install && npm run build` as the
build command and `npm start` as the start command — `next start` already picks up
Render's `PORT` env var automatically.

1. Push this repo to GitHub/GitLab and connect it in the [Render dashboard](https://dashboard.render.com/blueprints) as a new Blueprint.
2. Render will detect `render.yaml` and provision a Web Service rooted at `Jules-fireflies/naiom-platform`.
3. Fill in the env vars flagged `sync: false` in `render.yaml` (only `ANTHROPIC_API_KEY` is required — every other var unlocks one specific agent's integration and can be left blank).
4. If you use the Google integration (Gmail/YouTube agents), set `GOOGLE_REDIRECT_URI` to `https://<your-render-service>.onrender.com/api/integrations/google/callback`.
5. `OWNED_AGENT` is intentionally **not** set in `render.yaml` — leaving it unset unlocks all 14 agents. Set it to a single agent slug (e.g. `fireflies`) if you want to ship a single-agent template instead (see `src/lib/agents.ts`).

**Storage caveat**: several agents (Google/Arcads OAuth tokens, generated carousels/thumbnails/shorts/images, content library, prospection/veille/ecommerce data) write to local files under `src/data/` and `public/generated-*`. Render's default Web Service filesystem is **ephemeral** — everything written there is wiped on every deploy/restart and isn't shared across instances. That's fine for a quick demo, but for real use you'll want a [Render Disk](https://render.com/docs/disks) mounted over those paths (or to move that state to a database) so it survives redeploys.

Check out the [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying) for more general details.
