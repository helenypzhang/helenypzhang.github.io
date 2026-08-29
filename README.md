# Yupei Zhang — Academic Homepage

Source for [helenypzhang.github.io](https://helenypzhang.github.io/), built with [PRISM](https://github.com/xyjoey/PRISM), Next.js, TypeScript, and Tailwind CSS.

## Local development

Node.js 22 or later and pnpm are required.

```bash
pnpm install
pnpm dev
```

## Content

- English content: `content/`
- Chinese content: `content_zh/`
- Publications: `content/publications.bib`
- Images and PDFs: `public/`

Run `pnpm build` to create the static site in `out/`. Pushes to `main` are deployed automatically through GitHub Actions.

The current public CV is the 2025 version and can be replaced at `public/data/cv_yupeizhang_2025.pdf` when the updated CV is ready.
