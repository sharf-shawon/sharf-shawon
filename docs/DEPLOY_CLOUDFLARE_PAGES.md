# Cloudflare Pages Deployment

This project is ready to deploy on Cloudflare Pages as a Hugo site.

## Recommended Pages Settings

- **Framework preset**: `Hugo`
- **Build command**: `hugo --gc --minify`
- **Build output directory**: `public`
- **Root directory**: `/` (repo root)

## Required Project Settings in Cloudflare Pages

1. In your Pages project, connect this GitHub repository.
2. Enable **Build with submodules** (required for `themes/PaperMod`).
3. Set these environment variables:
   - `HUGO_VERSION=0.152.2`
   - `HUGO_ENV=production`

## Local Validation

```bash
git submodule update --init --recursive
hugo --gc --minify
```

If the build succeeds, deploy should produce the static site in `public/`.

## Notes

- `wrangler.toml` is included to declare `pages_build_output_dir = "public"` for Wrangler/Pages tooling.
- If you use the Cloudflare dashboard UI, keep the same build command and output directory.
