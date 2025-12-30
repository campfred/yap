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
npx blowfish-tools new $website_name
```

Source: [Blowfish docs: Getting started > Installation > Blowfish Tools (recommended)](https://blowfish.page/docs/installation/#blowfish-tools-recommended)

### Update the site

```shell
brew update hugo
brew update fnm
fnm install v24
fnm use v24
npx blowfish-tools update
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

Use [SVG Crop](https://svgcrop.com) to remove blank space around SVG icons.

## References

- [Blowfish docs](https://blowfish.page) [<sup>(archive)</sup>](https://web.archive.org/web/20251216160344/https://blowfish.page/)
  - [Icons](https://blowfish.page/samples/icons/) [<sup>(archive)</sup>](https://web.archive.org/web/20251017093620/https://blowfish.page/samples/icons/)
  - [Markdown](https://blowfish.page/samples/markdown/) [<sup>(archive)</sup>](https://web.archive.org/web/20251112170608/https://blowfish.page/samples/markdown/)
    - [Raw](https://raw.githubusercontent.com/nunocoracao/blowfish/refs/heads/main/exampleSite/content/samples/markdown/index.md)
  - [Shortcodes](https://blowfish.page/docs/shortcodes/) [<sup>(archive)</sup>](https://web.archive.org/web/20251221034138/https://blowfish.page/docs/shortcodes/)
- [CSS named colours organized by palette](https://austingil.com/every-css-named-color-organized-by-palette/) [<sup>(archive)</sup>](https://web.archive.org/web/20251230152105/https://austingil.com/every-css-named-color-organized-by-palette/)
- [Pictogrammers Material Design Icons](https://pictogrammers.com/library/mdi/)