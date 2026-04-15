# jimeng-cli

[简体中文说明](./README.zh-CN.md)

API-first CLI for Jimeng image and video generation, credit lookup, model listing, and result download.

## Features

- Load authentication from a Netscape cookie file.
- Submit Jimeng image and video generation jobs over HTTP APIs.
- Wait for task completion automatically when downloading generated assets.
- Inspect current credit balance.
- List the image and video model aliases supported by this CLI.

## Install

### Local development

```bash
npm install
```

### After publishing

```bash
npm install -g jimeng-cli
jimeng --help
```

## Quick start

```bash
# verify cookies
npm run dev -- auth check --cookie-file "G:\cookies\jimeng.txt"

# inspect credit balance
npm run dev -- credit --cookie-file "G:\cookies\jimeng.txt"

# list supported model aliases
npm run dev -- models

# submit image task only
npm run dev -- image generate "A neon fox in a cyberpunk city" --cookie-file "G:\cookies\jimeng.txt"

# submit and download image results
npm run dev -- image generate "A neon fox in a cyberpunk city" --download --cookie-file "G:\cookies\jimeng.txt"

# submit and download video results
npm run dev -- video generate "A glowing ship flying over a futuristic skyline" --download --cookie-file "G:\cookies\jimeng.txt"

# inspect recent history without creating a new job
npm run dev -- history list --limit 10 --cookie-file "G:\cookies\jimeng.txt"
```

## Commands

- `auth check` — validate the cookie file against Jimeng account info.
- `credit` — print current gift / purchase / VIP / total credits.
- `models` — print supported image and video model aliases.
- `image generate` — submit an image generation job.
- `video generate` — submit a video generation job.
- `task get` / `task wait` — inspect or wait for an existing task.
- `history list` — fetch existing generation history.
- `download` — resolve and download outputs for an existing task.

## Packaging notes

- The npm bin entry points to `dist/cli.js`.
- `npm pack` / `npm publish` will trigger `prepack`, which builds the project first.
- Only built artifacts and README files are included in the package tarball.

## Browser debugging fallback

The implementation is API-first. If request shapes change and browser-side debugging is needed, use this Chrome profile:

```text
G:\chrome_data\remote_debug
```

Use that profile only for DevTools verification and payload recovery, not as the primary execution path.
