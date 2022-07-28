### Intro to SASS

- Sass variables

- Nesting

- Partials and Imports

- Mixins

- functions

- interpolation

- Extending

- @-rules


#### Sass variables

````
$font-stack: Arial, Helvetica, sans-serif;
$light-color: #f4f4f4;
$primary-color: #0b82ab;
$secondary-color: #ff8700;
$fs-regular: 16px;

$colors: (
  light: #FFFFFF,
  dark: #000000,
  link: #428bca,
  linkHover: #555,
);

.my-class {
  font-size: $fs-regular;
  color: map-get($colors, dark);
}
````


#### Nesting
```
.showcase {
  @include set-background($primary-color);
  min-height: 100vh;
  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    ul {
      display: flex;
      list-style-type: none;
      li{
        padding: 15px;
        a {
          color: set-text-color($primary-color);
          &:hover {
            color: $secondary-color;
          }
        }
      }
    }
  }
  &-content {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 30px;
    img {
      width: 50%;
    }
    h1 {
      font-size: 50px;
      line-height: 1.2;
    }
  }
}

.funky {
  font: {
    family: fantasy;
    size: 30em;
    weight: bold;
  }
}
```
#### Partials and Imports

```
See inside project examplas
partials are created like sass files but with a "_" in forn of them. 
For example name of a partial will look like this. 
-> "_name.scss"

you can to import this file in another sass file or partial file using "@import"
for example

@import "_name.scss";

```

#### Mixins

```
@mixin <name> { 
  styling rules
} 

// or 

@mixin name(<arguments...>) { 
  styling rules
  styling rules <arguments...>
}

Example 

@mixin shape($width,$height,$color,$radius) {
    width: $width;
    height: $height;
    background: $color;
    border-radius: $radius;
}

.square {
    @include shape (350px,350px,red, 10px);
}

.circle {
    @include shape (200px,200px,green, 50%);
}



$light: 1px solid black;
$medium: 3px solid black;
$heavy: 6px solid black;
$none: none;

@mixin border-stroke($val) {
  @if $val == light
  {
    border: $light;
  }
  @else if $val == medium
  {
    border: $medium;
  }
  @else if $val == heavy
  {
    border: $heavy;
  }
  @else
  {
    border: $none;
  }
}

#box {
  width: 150px;
  height: 150px;
  background-color: red;
  @include border-stroke(heavy);
}

```

#### Functions

```

@function sqr($num) {
  @return #{$num * $num}px;
}

$squared: sqr(4);

body {
  font-size: $squared;
}


@function set-text-color($color) {
  @if(lightness($color) > 70) {
    @return #333;
  } @else {
    @return #fff;
  }
}

```

#### Interpolation

```
.showcase {
  @include set-background($primary-color);
  min-height: 100vh;
  &-content {
    #{&}-paragraph {
      font-size: $fs-regular;
    }
  }


@mixin corner-icon($name, $top-or-bottom, $left-or-right) {
  .icon-#{$name} {
    background-image: url("/icons/#{$name}.svg");
    position: absolute;
    #{$top-or-bottom}: 0;
    #{$left-or-right}: 0;
  }
}

@include corner-icon("mail", top, left);

```

#### Extending

```
%btn {
  display: inline-block;
  border-radius: 5px;
  padding: 8px 20px;
  margin: 3px;
  &:hover {
    transform: scale(.98);
  }
}

.btn-primary {
  @extend %btn;
  @include set-background(lighten($primary-color, 10%));
}

.btn-secondary {
  @extend %btn;
  @include set-background($secondary-color);
}

```

#### @-rules list

```
@use loads mixins, functions, and variables from other Sass stylesheets, and combines CSS from multiple stylesheets together.

@forward loads a Sass stylesheet and makes its mixins, functions, and variables available when your stylesheet is loaded with the @use rule.

@import extends the CSS at-rule to load styles, mixins, functions, and variables from other stylesheets.

@mixin and @include makes it easy to re-use chunks of styles.

@function defines custom functions that can be used in SassScript expressions.

@extend allows selectors to inherit styles from one another.

@at-root puts styles within it at the root of the CSS document.

@error causes compilation to fail with an error message.

@warn prints a warning without stopping compilation entirely.

@debug prints a message for debugging purposes.
       
Flow control rules like @if, @each, @for, and @while control whether or how many times styles are emitted.

```
