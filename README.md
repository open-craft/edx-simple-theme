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
* $main-nav-color
* $main-nav-link-color
* $main-nav-item-border-bottom-color
* $main-nav-item-hover-border-bottom-color
* $user-dropdown-color
* $customize-sign-in-btn. If defined, requires all the following variables to be set.
  - $btn-sign-in-bg
  - $btn-sign-in-color
  - $btn-sign-in-border-color
  - $btn-sign-in-hover-bg
  - $btn-sign-in-hover-color
  - $btn-sign-in-hover-border-color
* $customize-register-btn. If defined, requires all the following variables to be set.
  - $btn-register-bg
  - $btn-register-color
  - $btn-register-border-color
  - $btn-register-hover-bg
  - $btn-register-hover-color
  - $btn-register-hover-border-color
* $customize-logistration-btn. If defined, requires all the following variables to be set.
  - $btn-logistration-bg
  - $btn-logistration-color
  - $btn-logistration-border-color
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
