# Mixins

Mixins should _never_ contain actual CSS code but provide only Sass Code such as:

- `$variable`
- `@mixin`
- `@function`

This makes sure than a mixin can be `@use`d in other `.scss` files without 
causing Sass to generate duplicate code if style files are arbitrarily nested 
or refer to each other.

# Namespacing

Every Sass file can contain code that has the same name. Unless these files
are not included into the same target it all goes well. To make sure a variable
or mixin goes by a unique name. whenusing `@use` the file name is used as 
"namespace" for all the variables, functions and mxins therein.

The file `mixins/_device.scss` contains a variable names `$sizes` and so does
`mixins/_space_.scss`. In order to include both in a sass file the have to be 
namespaced:

In order to see what Sass is doing here, start Sass in watch mode and rename the
_partial_ `_namespace-demo.scss`  to `_namespace-demo.scss`.
You should see the `@debug` output.

```scss
@use "mixins/device";
@use "mixins/space";

// outputs the LIST $sizes
@debug device.$sizes;
// outputs the MAP $sizes
@debug space.$sizes;
```
