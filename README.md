# BRACA — Biodiversity Research and Conservation Alliance

A React + TypeScript + Vite wildlife research experience for biodiversity exploration, species profiles, field notes, habitats, and field operations.

## Local development

Requirements: Node.js 20.19+ or 22.12+.

```bash
npm install
npm run dev
```

Create and preview a production build:

```bash
npm run build
npm run preview
```

Run TypeScript checks with `npm run lint`.

## Deploy to Cloudflare Workers from GitHub

1. Push this project to a GitHub repository.
2. In Cloudflare, open **Workers & Pages → Create application → Workers** and connect the repository through Workers Builds, or deploy from a local terminal after authenticating Wrangler.
3. Use `npm install` as the install command, `npm run build` as the build command, and `npm run deploy` as the deploy command.
4. The included `wrangler.toml` publishes the Vite `dist/` folder as Cloudflare Workers Static Assets.

For a local deployment, run:

```bash
npm install
npm run build
npx wrangler login
npm run deploy
```

Cloudflare Pages is also supported: choose the Vite preset, build command `npm run build`, and output directory `dist`.

## Deployment and asset notes

- Wildlife imagery is served from `public/assets/wildlife/`, so image URLs remain valid after Vite builds the production site.
- The UI uses Motion for React transitions and respects reduced-motion preferences.
- Field-operation state currently uses browser local storage and the existing sync engine. Local storage alone is not a shared database; reliable cross-device persistence requires a configured sync transport or backend.
- Never commit secrets. `.env` files are ignored by Git.


## UI/UX refresh notes

- The mobile header now uses an accessible menu disclosure instead of a permanently scrolling navigation strip.
- Navigation closes after a destination is selected and uses the reduced-motion preference for scrolling.
- Motion for React (`motion/react`) powers the compact mobile-menu transition and the existing section/species transitions. Reduced-motion preferences are respected.
- Below-the-fold wildlife images use lazy loading and asynchronous decoding; the hero image is prioritized to reduce perceived loading time.
- The visual direction remains BRACA's forest-black, muted olive, ivory, and savanna-amber palette. The component approach is inspired by 21st.dev's React/Tailwind component patterns, but is implemented in the existing project rather than adding a separate component framework.

## Build verification

Run `npm install`, `npm run lint`, and `npm run build` before deployment. If your GitHub build uses Bun with a frozen lockfile, regenerate and commit `bun.lock` whenever `package.json` changes (`bun install`), otherwise the deployment can fail because the lockfile is out of sync.
