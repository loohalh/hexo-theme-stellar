# Stellar — a blog that can grow with your work

[English](README_EN.md) · [简体中文](README.md)

Stellar can begin as a quiet personal blog and grow into a home for your articles, project documentation, series, and notes.

[See the examples](https://xaoxuu.com/wiki/stellar/support/examples/) · [Getting started](https://xaoxuu.com/wiki/stellar/start/install/) · [Chinese documentation](https://xaoxuu.com/wiki/stellar/)

> The current Stellar v2 version is `2.0.0-rc.1`. Check npm and GitHub Releases for its public availability.

[![npm](https://img.shields.io/npm/v/hexo-theme-stellar)](https://www.npmjs.com/package/hexo-theme-stellar)
[![license](https://img.shields.io/github/license/xaoxuu/hexo-theme-stellar)](https://github.com/xaoxuu/hexo-theme-stellar/blob/main/LICENSE)
[![stars](https://img.shields.io/github/stars/xaoxuu/hexo-theme-stellar)](https://github.com/xaoxuu/hexo-theme-stellar)
[![npm downloads](https://img.shields.io/npm/dm/hexo-theme-stellar)](https://www.npmjs.com/package/hexo-theme-stellar)

## Four kinds of content, one site

Publish regular blog posts as usual. Give a project its own Wiki when it needs stable navigation. Keep a series of posts together as a Topic, or collect smaller pieces of knowledge in a Notebook.

They share the same navigation, search, sidebars, and reading experience. If all you need is a blog, the other systems stay out of the way.

## A static site with room for live data

Timelines, link status, remote README files, GitHub repositories and contributors, ratings, and polls can load when they are needed. Your site remains static, while frequently changing data does not require a full rebuild.

The article remains readable when a remote service is unavailable.

## Writing, finding, and reading belong together

Stellar includes content components for notes, folding sections, tabs, galleries, timelines, chat, tables, and more. Built-in local search can take a reader straight to a matching section. On smaller screens, navigation moves into drawers and leaves the page to the article.

## Choose a starting point

| Example | A good fit for |
| --- | --- |
| Light Blog | Essays, personal notes, and distraction-free reading |
| Blog | A classic sidebar blog with categories and series |
| Knowledge | A personal site combining articles and long-lived knowledge |
| Docs | Documentation for a single project |

The source for these sites lives in the catalog-driven [hexo-theme-stellar-examples](https://github.com/xaoxuu/hexo-theme-stellar-examples/) repository.

## Use the latest source

You need Node.js 22 or newer and Hexo 8 or newer. In the root of an existing Hexo site:

```bash
git submodule add -b main https://github.com/xaoxuu/hexo-theme-stellar.git themes/stellar
npm install --prefix themes/stellar
```

Enable the theme in `_config.yml`:

```yaml
theme: stellar
```

Then check and build the site:

```bash
npx hexo stellar doctor
npx hexo generate
```

The full v2 documentation is currently maintained in Chinese. The example repository provides an English quick start and complete runnable sites that can be explored without reading the whole reference.

## Stable npm release

```bash
npm install hexo-theme-stellar
```

This command may still install v1. Run `npm ls hexo-theme-stellar` before using any v2 configuration.

## Community

- [Issues](https://github.com/xaoxuu/hexo-theme-stellar/issues/) for reproducible problems
- [Discussions](https://github.com/xaoxuu/hexo-theme-stellar/discussions/) for ideas and usage questions
- [Contributing](CONTRIBUTING.md) for code and documentation work

## License

Stellar is free and open source under the [MIT License](LICENSE). Third-party licenses are listed in [THIRD-PARTY-NOTICES.md](legal/THIRD-PARTY-NOTICES.md).
