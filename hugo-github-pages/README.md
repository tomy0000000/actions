# Hugo GitHub Pages

Build Hugo site for GitHub Pages.

## Usage

```yml
name: 🚀 Deploy

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: true

defaults:
  run:
    shell: bash

jobs:
  build:
    name: 🛠 Build
    runs-on: ubuntu-latest
    steps:
      - name: 🛒 Checkout
        uses: actions/checkout@v3
        with:
          submodules: recursive

      - name: 🏗️ Build site
        uses: tomy0000000/actions/hugo-github-pages@main

  deploy:
    name: 🚀 Deploy
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: 🚀 Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v1
```

## Reference

- [actions/checkout](https://github.com/actions/checkout)
- [peaceiris/actions-hugo](https://github.com/peaceiris/actions-hugo)
- [actions/configure-pages](https://github.com/actions/configure-pages)
- [actions/upload-pages-artifact](https://github.com/actions/upload-pages-artifact)
- [actions/deploy-pages](https://github.com/actions/deploy-pages)
