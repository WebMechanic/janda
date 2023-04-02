# Sass Sources

Sass files (.scss/.sass) contain regular CSS code and call Sass features such as:

- `$variable`
- `@mixin`
- `@function`
- Sass Modules (`sass:math`, `sass:string` etc.)

## Partials

A file starting with an unterscore `_` is called a "partial" as it only 
contains styles with a very narrow scope, like the style rules for

- layouts/_blocks.scss &mdash; boxes and common areas
- pages/_login.scss &mdash; login page
- pages/_profile.scss &mdash; user profile
- pages/_home.scss &mdash; homepage
- forms/_forms.scss &mdash; forms (like a user + password combo)
- forms/_inputs.scss &mdash; input controls

They are the "module" and "component" styles for the various building blocks
of a site's pages.

A special partial named `_index.scss` can be used as a stand-in for the contents
of a complete folder. This is useful if many if the Sass sources in that folder 
should always be included as a whole. Adding the `_index.scss` file name is not
required to include "the folder".

```
/page-1.scss
/modules/_index.scss
/modules/_module-1.scss
/modules/_module-2.scss
/modules/_module-3.scss
```

The `_index.scss` file represents a fixed selection of files from its folder.
Sass will find the `_index.scss` if only the folder name is given in a `@use`
or `@forward` statement and read this file automatically.

```scss
// /modules/_index.scss
@forward "module-1";
@forward "module-2";
@forward "module-3";
```

```scss
// page-1.scss
@forward "modules"; // will include all three _module partials.
```

> To create a dedicated CSS file from the Sass sources of a folder use 
> `index.scss` instead (no underscore) and Sass will bundle it into a `index.css`.

## Bundled Stylesheets

Partials are eventually combined/bundled using a set of `@forward` rules
(the successor of `@import`) within Sass files that **do not** start with 
an underscore, like:

- /scss/styles.scss
- /scss/theme.scss
- /scss/home.scss
- /scss/login.scss

This is what a command like `sass scss:css` will eventually do.
Sass will transform these bundled styles from the `scss`folder into their 
.css (and .map) counterpart of the `css` target folder to be loaded 
by the browser.

- /css/styles.css
- /css/theme.css
- /css/home.css
- /css/login.css

## Multiple CSS files by combining different Sources

Another common use case is creating unprefixed .scss files inside a folder to
combine a specific set of partials into one .css file. Having separate
partials allows to reuse them to produce different CSS target files.

```
/scss/navigation
  - index.scss
  - mobile.scss
  - _menu.scss
  - _main-menu.scss
  - _hamburger.scss
```

Basic menu styles used by different Menu Components:

```scss
// navigation/_menu.scss - basic styles
@use "../mixins/space";

nav {
  padding: space.$md;
}

.menu {
  list-style: none;
}

:any-link {
  padding
  text-decoration: underline;
}
```

Main Menu Component styles from `navigation/index.scss`:

```scss
// navigation/index.scss
@forward "menu";
@forward "main-menu";
```

```scss
// navigation/_main-menu.scss - main menu
@use "../mixins/space";
@use "../mixins/theme";

.menu-main {
  padding: space.$sm;
  margin-block: space.$sm;
  > li.menu-item { 
    list-style: none;
    display: inline-block;
  }
  li :any-link {
    display: inline-block;
    padding: space:$xs;
    text-decoration: none:
  }
}
```

Mobile Menu Component styles from `navigation/mobile.scss`:

```scss
// navigation/mobile.scss
@forward "menu";
@forward "hamburger";
```

```scss
// navigation/_hamburger.scss - mobile menu
@use "../mixins/space";
@use "../mixins/theme";

.hamburger {
  position: sticky;
  top: space.$md;
  right: space.$md;
  padding: space.$sm;

  button {}
  svg {}
}
```

Sass will create two separate .css files the can be loaded into the .html

- /css/navigation/index.css
- /css/navigation/mobile.css

```html
<link href="css/style.css" rel="stylesheet">
<link href="css/theme.css" rel="stylesheet">

<!-- Main Menu Styles -->
<link href="css/navigation/index.css" rel="stylesheet">
<!-- Mobile Menu Styles (conditional loading) -->
<link href="css/navigation/mobile.css" rel="stylesheet" media="screen and (max-width:50rem)">
```
