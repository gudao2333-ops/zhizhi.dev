# Hexo + AnZhiYu

This project is initialized for Hexo with the `anzhiyu` theme and is ready for Cloudflare Pages deployment.

## Local development

```bash
npm install
npm run server
```

## Build

```bash
npm run build
```

The static output will be generated in `public/`.

## Cloudflare Pages settings

- Framework preset: `None`
- Build command: `npm run build`
- Build output directory: `public`
- Root directory: `/`

Cloudflare Pages can read the Node version from `.node-version`.

## Domain

- Production site: `https://zhizhi.dev`

## Publish checklist

1. Create a new GitHub repository.
2. Push this folder to the `main` branch.
3. Import the repository into Cloudflare Pages.
4. Use the build settings above.
5. After the first successful deploy, add the custom domain `zhizhi.dev` in Cloudflare Pages.
6. Confirm the DNS record in Cloudflare points to the Pages project.

## Common local commands

```bash
npm run server
npm run build
```
