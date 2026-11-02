# Carolina Pinto · Cybersecurity Portfolio

Built with Jekyll and the [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme, hosted on GitHub Pages.

## Where things live
| What | Where |
|---|---|
| Site name, links, color skin | `_config.yml` |
| Top menu | `_data/navigation.yml` |
| Home page & professional statement | `index.html` |
| Projects (one file each) | `_projects/` (images in `assets/images/projects/`) |
| Blog posts | `_posts/YYYY-MM-DD-title.md` |
| Resume | `_pages/resume.md` (+ `assets/resume.pdf`) |
| Custom colors / styles | `assets/css/main.scss` |

## Adding a project
Copy any file in `_projects/`, rename it, and edit the front matter
(`title`, `excerpt`, `project_category`, `order`, `featured`, `header.teaser`, `skills`, `project_url`).

## Adding a blog post
Create `_posts/2026-11-02-my-post-title.md`:
```yaml
---
title: "My Post Title"
categories: [GRC]
tags: [nist, risk]
---
Post content in Markdown…
```
