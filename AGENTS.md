# AGENTS.md

Welcome to **pratik280.github.io**, a static personal portfolio, blog, and knowledge base built primarily using **Vimwiki** for authoring content and compiling to HTML, served via GitHub Pages.

---

## 1. Architecture and Module Responsibilities

This repository operates as a static site generated from source documentation and templates.

- **`vimwiki/`**: The primary source directory containing all raw content written in Vimwiki markup (`.wiki`). This includes:
  - **`index.wiki`**: Portfolio homepage and main navigation hub.
  - **`about.wiki`**, **`resume.wiki`**, **`principles.wiki`**: Core static pages.
  - **`blogs/`**: Technical blog posts and articles.
  - **`notes/`**: Personal study notes, distributed systems references (Kafka, Java, AI-assisted coding, etc.).
- **`templates/`**: Layout templates and styling assets used to transform wiki markup into cohesive HTML pages (`default.tpl`, `style.css`).
- **HTML root files & subdirectories (`index.html`, `blogs/`, `notes/`, etc.)**: Compiled static outputs served directly by GitHub Pages.
- **`archived_old_blogs/`**: Legacy markdown-based blog posts and assets preserved for archival reference.

---

## 2. Technology Stack and Versions

- **Content Authoring**: Vimwiki
- **Templating / Compilation**: Vim / Vimwiki HTML export engine (or equivalent manual/scripted wiki compilation)
- **Styling**: Vanilla CSS (`style.css`, responsive layout design)
- **Hosting & Deployment**: GitHub Pages (static file serving)
- **Local Development Server**: Python 3 (`http.server`)

---

## 3. Naming and Coding Conventions

- **File Naming**: 
  - Use lowercase letters, hyphens (`-`) for word separation in file names (e.g., `how-i-think-about-kafka-partitions.wiki`).
  - `.wiki` extension for source files; corresponding `.html` files mirror the directory structure.
- **Markup Style**: 
  - Adhere to standard Vimwiki syntax (headers `= Header =`, lists `*`, links `[[page|Title]]`).
- **CSS / Templates**:
  - Keep styling modular, clean, and minimal. Use standard CSS custom properties or straightforward selectors.

---

## 4. Exception Handling and Logging Standards

- **Static Site Context**: Since this is a pure static site rendered to HTML, there is no runtime backend code, server-side exceptions, or application logging frameworks.
- **Build / Link Integrity**: 
  - Ensure all internal Vimwiki links use correct relative paths and valid targets to prevent 404 broken links upon HTML compilation.

---

## 5. Build, Test and Deployment Commands

### Local Development Server
To preview the generated static site locally:
```bash
python -m http.server 8000
```
Then open `http://localhost:8000` in your browser.

### Compilation / Publishing Flow
1. Edit content inside the `vimwiki/` directory.
2. Export/compile wiki files to HTML (via Vimwiki export commands or generator script).
3. Commit both source `.wiki` files and compiled `.html` output files to Git.
4. Push to `main` branch to automatically publish via GitHub Pages.

---

## 6. Existing Design Decisions and Constraints

- **Static Generation**: Zero client-side JavaScript frameworks or complex build pipelines (like React/Astro/Next.js) are used, ensuring blazing-fast load times, zero maintenance overhead, and seamless hosting on GitHub Pages.
- **Plain Text First**: Relying on Vimwiki keeps note-taking and blogging fast, frictionless, and tightly integrated with a Vim/Neovim editing workflow.
- **Archival Preservation**: Older blog posts (`archived_old_blogs/`) are kept intact for historical continuity without cluttering the active Vimwiki source tree.
