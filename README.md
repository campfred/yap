# Camp's yaps repository

All the source files of my blog that's hosted at [yap.jackle.ca](https://yap.jackle.ca) and will be replacing the [Carrd](https://carrd.co)-hosted one.

## Helpful commands

### Create the blog from scratch

This is more some personal notes here of how I did it because I have some special limitations on my machine that I use to write this blog.

```shell
brew install hugo
brew install fnm
fnm install v24
fnm use v24
npx blowfish-tools
```

Source: [Blowfish docs: Getting started > Installation > Blowfish Tools (recommended)](https://blowfish.page/docs/installation/#blowfish-tools-recommended)

### Update the site

```shell
git submodule update --remote --merge
```

### Serve the site locally with draft and future posts

```shell
hugo serve --buildDrafts --buildFuture
```

Source: [Blowfish docs: Getting started > Installing updates > Update using Hugo](https://blowfish.page/docs/installation/#update-using-hugo)

## Helpful tips for adding content

### Adding custom icons

1. Place an SVG file into the [assets/icons] folder
2. Open the file for editing
3. Remove all fill colour properties
4. Add a `fill="currentColor"` attribute in the `svg` tag

## References

- [Blowfish docs](https://blowfish.page)
  - [Icons](https://blowfish.page/samples/icons/)
  - [Markdown](https://blowfish.page/samples/markdown/)
    - [Raw](https://raw.githubusercontent.com/nunocoracao/blowfish/refs/heads/main/exampleSite/content/samples/markdown/index.md)
  - [Shortcodes](https://blowfish.page/docs/shortcodes/)
