# Clarity — Capstone portfolio entry

## Project brief

Clarity helps people turn a rough workplace or personal message into a clear, considerate draft without losing their intent. It is for anyone who pauses before sending a sensitive update, rescheduling request, or response and wants practical help finding the right words. I chose this idea because communication friction is common, emotionally real, and a good fit for AI’s strength—restructuring language—while still requiring the sender to own the final message.

## Product and repository

- **Live application:** Deploy `dist` to Vercel or Netlify, then paste the URL here: ____________________
- **Repository:** Publish this folder to GitHub/GitLab, then paste the URL here: ____________________
- **Setup:** `npm install && npm run dev`

## AI integration

The main workflow sends a rough message plus chosen audience and tone to Claude. A constrained prompt requires JSON with a subject, rewrite, and rationale notes; the client validates that response before display. The prompt explicitly prohibits invented facts, dates, people, links, or commitments. On absent configuration the app stays usable in a labelled local safe mode; service errors and malformed output show accessible errors without destroying input.

## Evidence

- **Unit tests:** `npm test` → 2/2 passing (validation and successful refinement flow).
- **Production build:** `npm run build` → succeeds.
- **Accessibility:** semantic labels, fieldsets/legends, native radio inputs, visible focus treatment, skip link, live status region, loading state, and inline errors are included. Run axe/WAVE and Lighthouse on the final deployed URL and attach the resulting screenshots here before submission.
- **Concrete audit-driven improvement:** custom-looking audience/tone controls retain native radio semantics and keyboard focus instead of replacing them with non-semantic clickable `div`s.

## Deployment and operations

The checked release checklist and rollback plan are in `DEPLOYMENT_CHECKLIST.md`. For public production, Claude calls must move to a serverless endpoint with the API key in protected host environment variables; add request limits and monitoring (e.g. Sentry). Roll back by promoting the prior successful deployment in the hosting dashboard.

## Reflection

The hardest part was making a generative model dependable enough for a small product. The model response cannot be trusted as a UI contract, so I constrained it to structured JSON, validated it, and designed for failure rather than treating it as an exception. I would set up the server-side boundary and monitoring earlier next time—doing it at the end turns a security decision into a release blocker. The most surprising learning was that accessible design improved the product’s tone: direct labels, useful validation, and explicit waiting states make a tool feel calmer and more trustworthy for every user.
