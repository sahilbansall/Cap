# Clarity

**Clarity** is an AI-assisted rewriting tool for anyone who wants to turn a rough message into a clear, considerate draft. It is intentionally small: the core job is helping a user communicate a sensitive update, request, or reply more effectively without erasing their voice.

> Live URL: add your Vercel/Netlify URL after deployment.  
> Repository: add your GitHub repository URL after publishing.

## Run locally

Requirements: Node.js 20+.

```bash
npm install && npm run dev
```

Open the local URL Vite prints. The application works without configuration in a safe local fallback mode. To enable Claude, copy `.env.example` to `.env.local` and add an Anthropic API key. Do not commit that file.

## Architecture

| Part | Responsibility |
| --- | --- |
| `src/App.jsx` | Accessible form, input validation, UI state, results, and copy interaction. |
| `src/ai.js` | Claude request, strict JSON validation, and safe offline fallback. |
| `src/styles.css` | Responsive layout, visible focus states, color contrast, and reduced visual complexity. |
| `src/App.test.jsx` | Component-level validation and successful rewrite flow. |

## AI integration

Claude is the actual rewriting engine—not a side chat. The user supplies a rough message, intended audience, and tone; the app sends these to a constrained system prompt. The model must return JSON with a subject, rewrite, and short explanation notes. The response is parsed and validated before rendering, so malformed model output becomes a useful error state instead of broken UI.

The prompt asks Claude to preserve meaning and never invent names, dates, commitments, links, or facts. When no API key is present, Clarity clearly marks its deterministic local safe mode and preserves the original text. This makes the demo functional and privacy-conscious during local development.

**Production note:** Browser-side API keys are suitable only for an educational demo. Before a public deployment, move `improveMessage` to a serverless function, store `ANTHROPIC_API_KEY` in the host’s encrypted environment variables, apply rate limits, and add authentication or a spending cap.

## Quality checks

```bash
npm test
npm run build
```

Tests cover the component’s validation state and the successful refinement flow. Run an axe or WAVE scan against the deployed page before submission. The concrete accessibility improvement already included is radio controls that retain native semantics while presenting an easy-to-scan chip UI, plus a visible keyboard focus indicator and skip link.

## Deployment and operations

Deploy to Vercel or Netlify with build command `npm run build` and publish directory `dist`. See [DEPLOYMENT_CHECKLIST.md](./DEPLOYMENT_CHECKLIST.md) for the release checklist and rollback plan.

Failures are contained: short inputs are explained inline, network/model errors leave the form intact with an alert, malformed AI responses are rejected, and absent AI configuration falls back locally. Monitor host function errors and client errors (e.g. Sentry); rollback by redeploying the last successful production build from `main`.

## Limitations and next steps

- An API key must be moved server-side before a public production release.
- The fallback preserves text rather than providing a model-quality rewrite.
- Add automated axe and end-to-end coverage, user accounts, rate limiting, and a server-side audit-safe analytics event for failures.

## Reflection

The hardest trade-off was making AI feel useful while keeping the application dependable. A free-form model response is not a stable UI contract, so I treated it as untrusted data: constrained prompt, JSON-only response, validation, and an error state. Next time I would start with a serverless API route from day one, because it protects credentials and creates a natural place for rate limits and observability. The surprising lesson was that accessibility choices made the product clearer for everyone: labels, focus states, helpful validation, and explicit loading feedback make the experience easier to trust—not just easier to navigate with assistive technology.
