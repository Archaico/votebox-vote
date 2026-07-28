# VoteBoxApp — Proposal Sharing Landing Page

The deep-link landing page for shared VoteBoxApp proposals. When someone taps a
shared proposal link and doesn't have the app installed, they land here instead
of a dead end.

**Live at:** https://vote.voteboxapp.org

## What it does

- Reads a proposal ID from the URL (`/proposal/{id}`)
- Fetches the proposal directly from Cardano (via Blockfrost) and IPFS (via
  Pinata/public gateways) — no backend server, no database
- Renders the proposal's title, description, live vote counts, and status
- Offers a direct APK download for anyone who wants to install VoteBoxApp and
  participate

## How it fits together

This is one piece of VoteBoxApp's link-sharing flow:

1. A user shares a proposal from the app — the link points here
   (`vote.voteboxapp.org/proposal/{id}`)
2. If VoteBoxApp is installed, Android's App Links open the app directly —
   this page never loads
3. If it isn't installed, this page loads instead and shows the proposal plus
   a download link

## Tech

Plain HTML/CSS/JS, no build step, no framework — hosted on GitHub Pages with a
custom domain. Reads Cardano data via Blockfrost's public API and proposal
content from IPFS.

## Android App Links verification

`.well-known/assetlinks.json` is required for Android to open the VoteBoxApp
app directly instead of this web page when it's installed. This repo also
needs a `.nojekyll` file at the root — GitHub Pages' default Jekyll build
step silently excludes any dot-prefixed path (including `.well-known`), so
without it, `assetlinks.json` 404s even when correctly committed.

## Main app

The mobile app itself lives at
[github.com/Archaico/VoteBoxApp](https://github.com/Archaico/VoteBoxApp).

---
AGPLv3 — part of the [VoteBoxApp](https://voteboxapp.org) project by the
LifeGround Community.
