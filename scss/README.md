# Sass Sources

Sass Sources contain regular CSS code and call Sass features such as:
- `$variable`
- `@mixin`
- `@function`
- Sass Modules (`sass:math`, `sass:string` etc.)

## Partials

A file starting with an unterscore `_` is called a "partial" as it only 
contains styles with a very narrow scope, like the style rules for

- layouts/_blocks.scss -- boxes and common areas
- pages/_login.scss -- login page
- pages/_profile.scss -- user profile
- pages/_home.scss -- homepage
- forms/_forms.scss -- forms (like a user + password combo)
- forms/_inputs.scss -- input controls

They are the "module" and "component" styles for the various building blocks
of a site's pages.

## Bundled Stylesheets

Partials are eventually combined/bundled using a set of `@forward` rules
(the successor of `@import`) within files that **do not** start with 
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

Aother common use case is creating an `index.scss` inside a folder that 
combines a set of partials inside into a whole .css file. Having separate
partials allows to reuse them for different CSS targets. 

```
/navigation
  - index.scss
  - mobile.scss
  - _menu.scss
  - _main-menu.scss
  - _hamburger.scss
```

```scss
// index.scss
@forward "menu";
@forward "main-menu";
```

```scss
// mobile.scss
@forward "menu";
@forward "hamburger";
```

```scss
// _menu - basic styles
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

```scss
// - _main-menu
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

```scss
// _hamburger
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
