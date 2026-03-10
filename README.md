# Gerard's Blog

Source for [blog.gerard.space](https://blog.gerard.space/). Built with Hugo, managed with Hermit. Feel free to use the theme for your own site!

## Development

1. `git clone https://github.com/casassg/blog && cd blog`
2. `source ./bin/activate-hermit`
3. `./bin/hugo server --buildDrafts`

## Deploy

1. Push changes to `main`.
2. GitHub Actions builds and deploys Hugo to GitHub Pages automatically.

Deployment is done automatically by [GitHub Pages](https://pages.github.com/) via `.github/workflows/hugo-pages.yml`, using Hugo from Hermit (`./bin/hugo`).
