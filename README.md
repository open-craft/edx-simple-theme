# Open edX Simple theme

This skeleton theme is used to customize the themes of Open edX instances using the `simple-theme` role from the `edx/configuration` repository.

## List of available SASS variables for customization

Below is the list of available SASS variables for customization. Check `lms/static/sass/theme-overrides.scss` for the details of what these variables are used for and as the authoritative source for the list of variables.

* $link-color
* $header-bg
* $customize-header-border (boolean). If defined, requires all the following variables to be set.
  - $header-border-top-width
  - $header-border-top-color
  - $header-border-bottom-width
  - $header-border-bottom-color
* $customize-footer-border (boolean). If defined, requires all the following variables to be set.
  - $footer-border-top-width
  - $footer-border-top-color
  - $footer-border-bottom-width
  - $footer-border-bottom-color
* $btn-font-size
* $btn-font-weight
* $btn-border-width
* $btn-primary-bg
* $btn-primary-color
* $btn-primary-font-size
* $btn-primary-font-weight
* $btn-primary-border-color
* $btn-primary-border-width
* $btn-primary-hover-bg
* $btn-primary-hover-color
* $btn-primary-hover-border-color
* $btn-secondary-bg
* $btn-secondary-color
* $btn-secondary-font-size
* $btn-secondary-font-weight
* $btn-secondary-border-color
* $btn-secondary-border-width
* $btn-secondary-hover-bg
* $btn-secondary-hover-color
* $btn-secondary-hover-border-color
* $main-nav-color
* $main-nav-link-color
* $main-nav-item-border-bottom-color
* $main-nav-item-hover-border-bottom-color
* $user-dropdown-color
* $customize-sign-in-btn. If defined, requires all the following variables to be set.
  - $btn-sign-in-bg
  - $btn-sign-in-color
  - $btn-sign-in-font-size
  - $btn-sign-in-font-weight
  - $btn-sign-in-border-color
  - $btn-sign-in-border-width
  - $btn-sign-in-hover-bg
  - $btn-sign-in-hover-color
  - $btn-sign-in-hover-border-color
* $customize-register-btn. If defined, requires all the following variables to be set.
  - $btn-register-bg
  - $btn-register-color
  - $btn-register-font-size
  - $btn-register-font-weight
  - $btn-register-border-color
  - $btn-register-border-width
  - $btn-register-hover-bg
  - $btn-register-hover-color
  - $btn-register-hover-border-color
* $customize-logistration-action-btn. If defined, requires all the following variables to be set.
  - $btn-logistration-bg
  - $btn-logistration-color
  - $btn-logistration-font-size
  - $btn-logistration-font-weight
  - $btn-logistration-border-color
  - $btn-logistration-border-width
  - $btn-logistration-hover-bg
  - $btn-logistration-hover-color
  - $btn-logistration-hover-border-color
* $login-register-header-color
* $accent-color
* $home-page-hero-title-color
* $home-page-hero-subtitle-color
* $wrapper-preview-menu-color
* $course-info-social-sharing-links-color
* $main-color
* $course-nav-menu-color
* $course-nav-menu-border-bottom-color
* $account-settings-nav-border-bottom-color
* $account-settings-nav-border-bottom-color
* $footer-bg
* $footer-color
* $footer-link-color

Of these variables,
* $main-color
* $link-color
* $header-bg
* $footer-bg
* $btn-primary-bg
* $btn-primary-color
* $btn-primary-border-color
* $btn-primary-hover-bg
* $btn-primary-hover-color
* $btn-primary-hover-border-color
* $btn-secondary-bg
* $btn-secondary-color
* $btn-secondary-border-color
* $btn-secondary-hover-bg
* $btn-secondary-hover-color
* $btn-secondary-hover-border-color

are required. All the other variables are optional.

To use on the devstack, you need to create `lms/static/sass/common-variables.scss` with the above
variables, and the file `lms/static/sass/_lms-overrides.scss` that imports these variables using
`@import 'common-variables';` and contains any other edx-platform-specific scss overrides.

You can then install and use it as a regular theme. Run `make dev.static.lms` to make
sure that the latest changes are picked up.

## Use as branding package for MFEs
This can also be used as a [branding package for MFEs](
  https://open-edx-proposals.readthedocs.io/en/latest/oep-0048-brand-customization.html).
To do so install this package as an override to `@edx/brand`. Any variables specified in
`lms/static/sass/common-variables.scss` will be picked up by the MFE as well.

If you're using `edx/configuration` for deployment, you can also have this theme applied to MFEs by
adding it as an npm override from the location where it's already installed. You can do so by adding
the following ansible config:

```yaml
MFE_DEPLOY_NPM_OVERRIDES:
  - "@edx/brand@file:/edx/var/edxapp/themes/simple-theme/"
```

## WIP: Usage with style dictionary / design tokens

Design tokens present a new way of customising styles using variables that are
then translated into different forms depending on the platform they are used in.

For instance a token like `color.brand.base` could translate to a SCSS variable
called `$brand-base` a css variable called `--pgn-color-brand-base` or be output
in an XML that can be used for styling Android. For now the focus of Paragon is
on CSS variables.

To customise a theme using this system, you'll need to provide all the variables
that you want to override in JSON files. You can look at the JSON files in the
Paragon repository ([currently in the alpha branch](https://github.com/openedx/paragon/tree/alpha/tokens/src)) to see how they are used and what all can be
customised.

In the `tokens/core` or `tokens/light` directories (light is the theme name, you
can have other names) you can create JSON files that override any of the values
in Paragon. You can see how these JSON files are structured at the link above.
While Paragon follows a strucure above, based on component names, the variable
type etc. This is not necessary, the exact structure doesn't matter, they are
all loaded and merged into one dictionary of styles and the output theme will
output it as CSS variables so they can be loaded by the custom theme.

This is a two-step process:

1. Building the tokens: The `paragon build-tokens` build tokens command compiles
   the JSON style dictionaries into CSS files in the `paragon/css/` directory.
   These are supposed to be committed to the repository.
2. Building the SCSS: The build token CSS files are then compiled into a brand
   theme in the dist folder using the `paragon build-scss` command. The contents
   of the dist directory are what needs to uploaded to the CDN and will be
   loaded by MFEs.

Unlike SCSS variables, which are evaluated at build time and then applied to a
theme, CSS variables are evaluated at run time. This means you can build a base
Paragon theme that is using CSS variables and then you can swap out the
stylesheet that defines all the variables to quickly change the theme at
runtime.

To use the custom theme, you no longer need to install the custom branding
package, instead you provide the theme stylesheet URLs via the MFE config API.
The built themes can be uploaded to a CDN and those URLs can be specified via
the MFE config API in the following format:

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
`brandOverride`. The default is the core theme whereas the `brandOverride` applies
on top. This keeps the theme smaller since you don't need to include and update
all the variables from the core theme.

In the above example when configuring the theme for an instance, you would
upload the `dist` folder contents to a CDN, and add the path to `core.min.css`
and `light.min.css` to the appropriate places. You can also create other themes
like a `dark` theme or a separate theme for each site.

NOTE: CSS variables are technically called CSS custom properties but they are
called variables here because that more closely corresponds with how they are
being used here.

## WIP: Automatically deploying a runtime theme to S3 via gitlab CI

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
