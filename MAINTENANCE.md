# Academic Homepage Maintenance Guide

This guide explains how to maintain Yupei Zhang's academic homepage: <https://helenypzhang.github.io/>.

Most routine updates only require editing these directories:

- `content/`: English content
- `content_zh/`: Chinese content
- `public/`: publication images, profile image, CV, and other public files
- `src/`: page components and styles; routine content updates normally do not require changes here

Except for the publication list, update the corresponding file in `content_zh/` whenever you change English content. This keeps the English and Chinese versions consistent. Publications are maintained only once in `content/publications.bib` and shared by both languages.

## 1. Add a News Item

English news is stored in `content/news.toml`. Chinese news is stored in `content_zh/news.toml`.

Add the newest item at the top of each file:

```toml
[[news]]
date = "2026-09"
content = "Our paper was accepted by ..."
```

Add the matching Chinese item to the Chinese file:

```toml
[[news]]
date = "2026-09"
content = "我们的论文被……接收。"
```

Use the `YYYY-MM` date format, for example `2026-09`.

The News area has a fixed maximum height. When the list becomes longer, it can be scrolled. Its scrollbar remains hidden until the pointer is over the News list or the list receives keyboard focus.

## 2. Add a Publication

Add every publication to `content/publications.bib`. Place a new entry near the top of the file. The website automatically sorts publications by year and month in descending order.

### Journal article example

```bibtex
@article{zhang2026example,
  selected = {true},
  title = {Paper Title},
  author = {Yupei Zhang# and Coauthor Name# and Senior Author},
  year = {2026},
  month = sep,
  journal = {Journal Name},
  url = {https://example.com/paper},
  code = {https://github.com/example/repository},
  preview = {example.png},
  description = {A short description of the paper.}
}
```

### Conference paper example

Use `@inproceedings` and put the conference name in `booktitle`:

```bibtex
@inproceedings{zhang2026conference,
  title = {Paper Title},
  author = {Yupei Zhang and Coauthor Name and Senior Author},
  year = {2026},
  month = oct,
  booktitle = {Conference Name},
  url = {https://example.com/paper},
  preview = {conference-paper.png}
}
```

### Preprint example

Use `@misc` or `@unpublished`:

```bibtex
@misc{zhang2026preprint,
  title = {Paper Title},
  author = {Yupei Zhang and Coauthor Name and Senior Author},
  year = {2026},
  month = sep,
  url = {https://arxiv.org/abs/xxxx.xxxxx},
  preview = {preprint.png}
}
```

### Custom publication fields

- `selected = {true}`: shows the paper in Selected Publications on the homepage. Remove this line or set it to `false` to show the paper only on the Publications page.
- `preview = {image-filename}`: sets the preview image. The image must be stored in `public/papers/`.
- `url`: sets the Paper button link. If `url` is omitted but `doi` is provided, the website generates a DOI link automatically.
- `code`: sets the Code button link. Remove this field when code is unavailable.
- `journal`: journal name.
- `booktitle`: conference name.
- `month`: use an English abbreviation such as `jan`, `feb`, or `mar`. This controls sorting within the same year.
- `description`: optional short description.
- The identifier at the beginning of each entry, such as `zhang2026example`, must be unique.

### Author markers

- Add `#` after a name to mark a co-first author. The website displays it as `*`.
- Add `*` after a name to mark a corresponding author. The website displays it as `†`.
- If no corresponding-author marker is provided, the final author is treated as the corresponding author.
- Separate authors with `and`.
- `Yupei Zhang` is highlighted automatically.

Example:

```bibtex
author = {Yupei Zhang# and First Coauthor# and Senior Author*}
```

## 3. Add or Replace a Publication Image

Copy the image into:

```text
public/papers/
```

Use the exact same filename in the publication entry:

```bibtex
preview = {my-paper-figure.png}
```

Recommendations:

- Use PNG, JPG, or WebP.
- A landscape image close to `16:10` works best. Other aspect ratios are supported and displayed without cropping.
- Use lowercase letters, numbers, and hyphens in filenames, for example `tmi-2026-framework.png`.
- When replacing an existing image, keeping the old filename avoids another content edit. Browser caching may require a short wait or a forced refresh after deployment.

## 4. Update the Biography and Research Interests

- English biography: `content/bio.md`
- Chinese biography: `content_zh/bio.md`
- English research interests: `research_interests` in `content/about.toml`
- Chinese research interests: `research_interests` in `content_zh/about.toml`

Example:

```toml
[profile]
research_interests = [
  "Multimodal Learning in Medicine",
  "Computational Pathology",
  "Medical Image Analysis",
  "Translational AI"
]
```

## 5. Update Name, Position, Contact Details, or Social Links

Edit the English information in `content/config.toml`. Chinese translations of the name, position, institution, location, and navigation labels are in `content_zh/config.toml`.

Common sections:

- `[author]`: name, position, institution, and profile image
- `[social]`: email, Google Scholar, GitHub, LinkedIn, and location
- `[site]`: site title, description, and last-updated date

The current profile image is set by `avatar = "/bio.png"`, which points to `public/bio.png`.

## 6. Update the Navigation Bar

English navigation is defined by the `[[navigation]]` blocks in `content/config.toml`. Chinese navigation is defined in `content_zh/config.toml`.

### Add an external link

For example, to add Google Scholar:

```toml
[[navigation]]
title = "Google Scholar"
type = "link"
target = "google_scholar"
href = "https://scholar.google.com/..."
```

Add the same item to the Chinese configuration and translate only `title` if necessary.

### Change the navigation order

Reorder the complete `[[navigation]]` blocks in both configuration files.

### Temporarily hide an item

Remove or comment out the corresponding `[[navigation]]` block in both language configurations. The page content can remain in the project and the navigation block can be restored later. The Awards page is currently retained but hidden this way.

## 7. Add a Standard Page

The simplest new page is a Markdown text page. For example, to add Teaching:

1. Create `content/teaching.md` with the English content.
2. Create `content_zh/teaching.md` with the Chinese content.
3. Create `content/teaching.toml`:

```toml
type = "text"
title = "Teaching"
description = "Teaching experience and activities."
source = "teaching.md"
```

4. Create `content_zh/teaching.toml`:

```toml
type = "text"
title = "教学"
description = "教学经历与活动。"
source = "teaching.md"
```

5. Add this block to `content/config.toml`:

```toml
[[navigation]]
title = "Teaching"
type = "page"
target = "teaching"
href = "/teaching"
```

6. Add the same block to `content_zh/config.toml` and translate `title`. Do not translate `target` or `href`.

After deployment, the page will be available at `/teaching/`.

## 8. Update Academic Services

- English page: `content/services.md`
- Chinese page: `content_zh/services.md`
- Page title and description: `services.toml` in each corresponding directory

Follow the existing Markdown format to add Conference Reviewer or Journal Reviewer entries.

## 9. Update the CV

The current CV is stored at:

```text
public/data/cv_yupeizhang_2025.pdf
```

To keep the public link unchanged, replace that PDF while retaining the same filename. If the filename changes, update the link in both `content/cv.md` and `content_zh/cv.md`.

## 10. Preview Locally

From the project directory, run:

```bash
pnpm install
pnpm dev
```

Open the local address shown in the terminal, usually <http://localhost:3000/>.

When finished, press `Control + C` in the terminal to stop the preview.

Before publishing, run:

```bash
pnpm build
```

A successful build confirms that the static website can be generated.

## 11. Publish to GitHub

The website is deployed automatically whenever the `main` branch is updated. A typical content-only update uses:

```bash
git status
git add content content_zh public
git commit -m "Update publications and news"
git push origin main
```

If other files were changed, add them explicitly or use `git add -A` after verifying that every change should be published.

After pushing, check the Actions page in the GitHub repository. Once the deployment finishes, refresh <https://helenypzhang.github.io/>. Deployment and browser caching can take a short time.

## 12. Pre-publication Checklist

- Update both English and Chinese content where applicable.
- Check the year, month, journal, or conference name for every new publication.
- Confirm whether `selected` matches the intended homepage visibility.
- Test Paper, Code, and DOI links.
- Confirm that each preview image is in `public/papers/` and that its filename matches the BibTeX entry.
- Check co-first author `#` and corresponding author `*` markers.
- Keep English and Chinese navigation configurations consistent.
- Confirm that `pnpm build` succeeds.
- Use `git status` to verify that only intended changes will be published.
