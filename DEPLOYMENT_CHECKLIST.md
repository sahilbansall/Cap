# Clarity deployment checklist

Use this checklist immediately before a production release.

- [ ] `npm test` passes locally.
- [ ] `npm run build` passes locally.
- [ ] Manual keyboard pass completed: skip link, input, radio buttons, submit, and copy action are usable.
- [ ] Mobile viewport checked at 320px width.
- [ ] Run axe or WAVE on the deployed URL; resolve all serious/critical issues.
- [ ] Run Lighthouse mobile audit; target ≥85 across Performance, Accessibility, Best Practices, and SEO.
- [ ] Confirm no secrets are committed and `VITE_ANTHROPIC_API_KEY` is not used in public production builds.
- [ ] Configure a server-side `ANTHROPIC_API_KEY`, request timeout, rate limit, and error monitoring before enabling AI publicly.
- [ ] Confirm the unavailable-service error and local safe fallback display correctly.
- [ ] Confirm deployment environment, domain, and HTTPS are correct.

**Sign-off:** ____________________  **Date:** ____________________  **Production URL:** ____________________

## Rollback

If a release causes a critical issue, use the hosting provider’s deployment dashboard to instantly promote the prior successful production deployment. Then open an issue with the failing URL, browser/device, timestamp, and affected flow. Re-enable new releases only after the issue is reproduced and the automated checks pass.
