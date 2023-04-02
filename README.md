# r1
 r1

april 2: 
TO COMPILE SCSS TO CSS (STYLE.SCSS --> STYLE.CSS)
using Windows Powershell or CMD.exe with command...

    sass --watch scss:css

Requires Dart Sass from https://github.com/sass/dart-sass/releases/tag/1.60.0 inside `PATH`

To make sure Sass tells about deprecated features run

    sass --future-deprecation import --watch scss:css

## Themeing

Use generic color names to simplify themeing. 
A variable `$black` might not have the value `#000` and remain truly black in another colour theme. 
Use `$dark` instead and whatever "dark" means in any given theme will always produce the correct **dark shade** and tint.

Useful, generic color names are:
- brand: the primary company brand color
- second: the secondary company brand color
- accent: an accented color, might be the same as $brand or $secondary
- compl: a complementary color for $brand

On their own as well as a prefix to the above:
- muted
- dimmed
- notice
- warning
- success
- error

## Color Ramps

The CSS color function [hwb()](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hwb) makes creating color ramps easy by simmply changing the **whiteness** or **blackness** of a color hue.

If different shades of a color are expected use number prefixed for each step.
Ten steps are usually sufficient for most use cases. Always keep step `-5` as the "normal" or "middle" value of a set even if there is no complete ramp _yet_. This allows room to go both lighter or darker later in the project w/o having to rewrite everything and still adhere to a "system".

```scss
// -1 is always the darkest color shade
$green-1: hwb(107 5% 75%);
$green-6: hwb(107 25% 25%);
// -10 is always the lightest color shade
$green-10: hwb(107 65% 5%);
```

For spacing and sizing adhere to the number system already in place for `font-weight`: 100 through 900, with 100 being the smallest and 900 the largest number. Increase insteps of `100` and if required add a `50` in between.

For white space in boxes and between elements using T-shirt sizes is also a common approach. Here the medium size (`md`) will be the default all sizes are in reference to. 

- `--spacer-xs`: 0.5em
- `--spacer-sm`: 1em
- `--spacer-md`: 1.625em
- `--spacer-lg`: 2.225em
- `--spacer-xl`: 3.325em

Font sizes:
- `--fs-sm`: 0.5em
- `--fs-md`: 1em
- `--fs-lg`: 1.625em
- `--fs-xl`: 2.225em
- `--fs-xxl`: 3.325em

If you need super extra extra small/large values then this system maybe wasn't the best idea but you can always add numbers:

- `--spacer-2xl`  `--spacer-2xs`
- `--spacer-3xl`  `--spacer-3xs`
- `--spacer-4xl`  `--spacer-4xs`
- `--spacer-5xl`  `--spacer-5xs`
