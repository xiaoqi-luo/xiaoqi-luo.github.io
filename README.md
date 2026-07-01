# luoxiaoqi.github.io

Personal academic website of **罗骁齐 (Xiaoqi Luo)**, built with the
[al-folio](https://github.com/alshedivat/al-folio) Jekyll theme. Tailored for
PhD applications and full-time research roles in embodied AI, multimodal
learning, and brain-computer interfaces. **The site is currently
Chinese-only** (`lang: zh-CN`).

## Site structure

| Page | Source | What to edit |
|------|--------|--------------|
| 关于 / Home | `_pages/about.md` | Bio, profile photo (`assets/img/prof_pic.jpg`) |
| 论文 / Publications | `_bibliography/papers.bib` | BibTeX entries |
| 项目 / Projects | `_projects/*.md` | One file per project/internship (category `工作`/`研究`) |
| 简历 / CV | `_pages/cv.md` | Hand-written Chinese markdown (self-contained) |
| CV (PDF) | `assets/pdf/cv_xiaoqi_luo.pdf` | Replace with your latest PDF |
| 动态 / News | `_news/*.md` | One file per announcement |
| Social links | `_data/socials.yml` | Email, GitHub, Scholar, … |
| Site identity | `_config.yml` | Name, URL, description, navbar |

> Note: `_data/cv.yml` (the RenderCV data source) is **no longer used** — the
> CV page is hand-written Chinese markdown in `_pages/cv.md`.

## TODO before going live

These items currently hold placeholders and should be replaced with real data:

1. **Papers** — `_bibliography/papers.bib`: replace `TODO` titles, co-authors,
   DOIs, abstracts, and `google_scholar_id` for both entries.
2. **Google Scholar ID** — `_data/socials.yml`: set `scholar_userid`.
3. **LinkedIn / ORCID** — `_data/socials.yml`: fill `linkedin_username`,
   `orcid_id`.
4. **Project teaser images** — `_projects/*.md` `img:` points to
   `assets/img/1..4.jpg` placeholders; replace with real screenshots/photos.
5. **Project videos** — each project page has a YouTube `VIDEO_ID` placeholder
   (and a commented `{% include video.liquid %}` for local files). Replace with
   real demo videos.
6. **CV PDF** — `assets/pdf/cv_xiaoqi_luo.pdf` is the current Chinese LaTeX CV.
7. **Profile photo** — `assets/img/prof_pic.jpg` (currently your WeChat photo).

## Local development

al-folio v1.x requires **Ruby ≥ 3.1** and **Node ≥ 20**.

```bash
bundle install
npm install
bundle exec jekyll serve --livereload
# open http://127.0.0.1:4000
```

The system Ruby on macOS (2.6) is too old. Use a newer Ruby via Homebrew/rbenv,
or just rely on the GitHub Actions build (see below).

## Deployment (automatic)

Pushing to `main` triggers `.github/workflows/deploy.yml`, which builds the site
with Jekyll and publishes `_site` to the `gh-pages` branch.

One-time GitHub setup:

1. Create a repo named **`luoxiaoqi.github.io`** (must match your GitHub
   username) and push this code to `main`.
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a
   branch → Branch: `gh-pages` / `/ (root)`**.
3. After the first Actions run finishes, the site is live at
   <https://luoxiaoqi.github.io>.

## License

al-folio is MIT-licensed; see `LICENSE`. Site content © Xiaoqi Luo.
