# MindML

## Overview

```
Create your own Wiki or digital garden for creating knowledge base
```
Host a simple technical website using `mkdocs-material` for notes and documentation.

Simple yet salient featrues to note are :
- Toggle between light and dark mode
- Search bar
- Support for `[[wikilinks]]`

## Inspiration

- [Notes on AI](https://notesonai.com/Notes+on+AI) is a personal wiki on AI and ML and deployed using `Obsidian-publish`.
- However, it is not free and requires a subscription to `Obsidian Publish` to host the wiki.
- This wiki is inspired by the above and is deployed using `mkdocs-material` and hosted on `Github Pages` for free (You can also host it on `Netlify`, `DigitalOcean` or `GitLabs`).
- Since, everyone loves VS Code, it made much more sense to use it rather than Obsidian.

## Setup

1. Markdown files are easy to write and can be easily converted to html which can be hosted online.
2. `Foam` : VS Code extension for `Obsidian` like experience. Enables wikilinks, graph visualization and backlinks in VS Code.
3. `mkdocs-material` : Material for MkDocs is a theme for MkDocs, a static site generator geared towards (technical) project documentation. It is a python package which be installed via pip.

## Usage
1. Change the `mkdocs.yml` file to add / remove any feature you want. It contains all the meta data of your site.
2. The `ci.yml` is used by github actions to deploy the site on github pages.
3. Make another branch named **gh-pages**.
4. Go to the repository. Then go to _Settings -> Pages -> Branch_. Set it to _gh-pages_.
5. Now, any changes you push to the main will automatically trigger deployment to github pages.
6. Now, just add your markdown files to the `docs` folder.
