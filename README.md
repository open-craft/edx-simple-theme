# Open edX Simple theme

This skeleton theme is used to customize the themes of Open edX instances using
the `simple-theme` plugin that's part of the
[`tutor-contrib-grove` plugin](https://gitlab.com/opencraft/dev/tutor-contrib-grove/)

## For Simple Theming Requirements

If the theme requirements are simple and only involve minor changes to theme
colors, spacing etc, then you can accomplish a lot using the
`grove-simple-theme` plugin that's a part of
[`tutor-contrib-grove`](https://gitlab.com/opencraft/dev/tutor-contrib-grove/).

Using that plugin you can provide override values for any design token and it
also includes a simple mechanism for overriding theme colors by automatically
generating lighter and darker variations.

## For Complex Theming Requirements

If more complex changes are needed that would require adding CSS classes, then
you can make a fork of this repository and put any customisations in the
`paragon/_customizations.scss` file.

Before considering a fork, see if the customisation can be supported upstream,
or in this repo in a way that it can be toggles on or off using tokens.

## Usage Without Simple Theme Tutor Plugin

The Tutor Simple Theme Plugin simply installs this package as an alias of
`@edx/brand` and then generates the token files for theming based on the tutor
config. For local testing or for more customised usage you can create the tokens
yourself in the correct folders and then build and install this package into an
MFE.

## Intro to Design Tokens Using Style Dictionary

Design tokens present a new way of customising styles using variables (called
tokens) that are then translated into CSS variables for loading in the platform.
Style Dictionary is a library by Amazon that enable the use of design tokens
using JSON files. It is the library Paragon is using for handling design tokens.

For instance a token like `color.brand.base` would translate to a css variable
called `--pgn-color-brand-base` which could then be used by any components.

To customise a theme using this system, you'll need to provide all the variables
that you want to override in JSON or TOML files. You can look at the JSON files
in the Paragon repository
([currently in the alpha branch](https://github.com/openedx/paragon/tree/alpha/tokens/src))
to see how they are used and what all can be customised.

In the `tokens/core` or `tokens/themes/light` directories you can create
JSON/TOML files that override any of the values in Paragon. You can see how
these JSON files are structured at the link above. While Paragon follows a
strucure above, based on component names, the variable type etc. this is not
strictly necessary. The exact structure doesn't matter, they are all loaded and
merged into one dictionary of styles and the output theme will output it as CSS
variables so they can be loaded by the custom theme.

You can create any number of themes in the `paragon/css/themes` directory,
`light` is just the default theme name.

This is a two-step process:

1. Building the tokens: The `paragon build-tokens` build tokens command compiles
   the style dictionaries into CSS files in the `paragon/css/` directory. These
   are supposed to be committed to the repository.
2. Building the SCSS: The build token CSS files are then compiled into a brand
   theme in the dist folder using the `paragon build-scss` command. The contents
   of the `dist` directory are what are loaded into the MFEs.

Unlike SCSS variables, which are evaluated at build time and then applied to a
theme, CSS variables are evaluated at run time. This means you can build a base
Paragon theme that is using CSS variables and then you can swap out the
stylesheet that defines all the variables to quickly change the theme at
runtime.

NOTE: CSS variables are technically called CSS custom properties but they are
called variables here because that more closely corresponds with how they are
being used here.

## Hosting the Theme CSS at a CDN.

To use the custom theme, you no longer need to install the custom branding
package, instead you provide the theme stylesheet URLs via the MFE config API.
The built theme files fromt the `dist` can be uploaded to a CDN and those URLs
can be specified via the MFE config API in the following format:

```json
{
  ...
  "MFE_CONFIG": {
    ...
    "PARAGON_THEME_URLS": {
      "core": {
        "urls": {
          "default": "https://cdn.jsdelivr.net/npm/@edx/paragon@$paragonVersion/dist/core.min.css",
          "brandOverride": "https://cdn.jsdelivr.net/npm/@edx/brand-edx.org@#brandVersion/dist/core.min.css"
        }
      },
      "defaults": {
        "light": "light"
      },
      "variants": {
        "light": {
          "urls": {
            "default": "https://cdn.jsdelivr.net/npm/@edx/paragon@$paragonVersion/dist/light.min.css",
            "brandOverride": "https://cdn.jsdelivr.net/npm/@edx/brand-edx.org@$brandVersion/dist/light.min.css"
          }
        }
      }
    }
  }
}
```

The above are the vanilla Paragon stylesheets. The core stylesheets contain the
bulk of the Paragon styling while the variants have the style variables that
modify how the core theme applies. For both of those you have a `default` and a
`brandOverride`. The default is the core theme whereas the `brandOverride`
applies on top. This keeps the theme smaller since you don't need to include and
update all the variables from the core theme.

In the above example when configuring the theme for an instance, you would
upload the `dist` folder contents to a CDN, and add the path to `core.min.css`
and `light.min.css` to the appropriate places. You can also create other themes
like a `dark` theme or a separate theme for each site.

## Automatically Deploying a Runtime Theme to S3 via Gitlab CI

This repo has a GitLab CI configuration to automatically deploy to AWS S3 if
configured.

To use that you need to configure the environment variables that AWS CLI needs
for S3. At minimum you need:

- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- S3_BUCKET

If deploying to DigitalOcean buckets or some other S3-compatible storage you can
specify `AWS_ENDPOINT_URL` as well.

If the files need to be deployed to a sub-path, set `THEME_PATH` as well. This
can be used to build and deploy themes to a CDN after changing design tokens to
update or fix a theme.

## Use as branding package for MFEs or comprehensive theme

Since the relevance of comprehensive theme is waning and won't see any updates
and MFEs will hard switch to design tokens only in the future, simple theme now
only supports design tokens, and is intended to be used with
`tutor-contrib-grove`. To use it as a branding package or comprehensive theme
use a branch for an older release.
