I would like to host my Obsidian notes for free on GitHub pages. To do this I am using Quartz to convert Obsidian markdown file sinto static webpages. This docukemtn outlines the resources I used to set up Quartz.

## Resources

- [How to publish your notes for free with Quartz](https://www.youtube.com/watch?v=6s6DT1yN4dw)
- [Quartz Docs](https://quartz.jzhao.xyz)
- [Quartz GitHub Project](https://github.com/jackyzha0/quartz)


## Server Quartz Locally

To Visualise the Quartz project locally you can run the following command from within in your Quartz project.

```bash
npx quartz build --serve
```

*Resource: [Building your Quartz](https://quartz.jzhao.xyz/build)*

## Hosting Quartz with GitHub Pages

1. Create `deploy.yml` file in `quartz/.github/workflows/`
2. Populate with the following content.

```yaml
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - v4
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v4
        with:
          node-version: 22
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: public
 
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4

```

3. Ensure that GitHub Pages source is set to 'GitHub Actions' (this is only available on free tier if your repository is made public.)

*Resource: [Hosting](https://quartz.jzhao.xyz/hosting)