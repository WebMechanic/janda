# Mixins

Mixins should _never_ contain actual CSS code but provide only Sass Code such as:

- `$variable`
- `@mixin`
- `@function`

This makes sure that a mixin can be `@use`d in other `.scss` files without 
causing Sass to generate duplicate code if the files are arbitrarily nested 
or refer to each other.

# Namespacing

Every Sass file can contain code that has the same name. Unless these files
are not included into the same target it all goes well. To make sure any variable
or mixin goes by a unique name when combined with `@use`, the file name serves as 
a "namespace" for all the variables, functions and mixins therein.

The file `mixins/_device.scss` contains a variable names `$sizes` and so does
`mixins/_space_.scss`. In order to include both in the same sass file they have to be 
namespaced.

In order to see what Sass is doing here, start Sass in watch mode 
`sass --watch scss:css` and have a look at `namespace-demo.scss`.
You should see several `@debug` messages in the console.

```scss
@use "mixins/device";
@use "mixins/space";

// outputs the LIST $sizes
@debug device.$sizes;
// outputs the MAP $sizes
@debug space.$sizes;
```
(the actual file contains many more @debug messages and demo code).
