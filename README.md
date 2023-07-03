# Open edX Simple theme

This skeleton theme is used to customize the themes of Open edX instances using the `simple-theme` role from the `edx/configuration` repository.

# List of available SASS variables for customization

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
* $main-color
* $course-nav-menu-color
* $course-nav-menu-border-bottom-color
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

# [IN DEVELOPMENT] Use as branding package for MFEs
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
