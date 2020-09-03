# Fundamentals

[Course Video](https://www.lynda.com/Sass-tutorials/What-you-should-know-before-watching-course/375925/435555-4.html?org=bpl.org)

[Github Repo](https://github.com/planetoftheweb/sassEssentials)

Project Files: /home/tim/GitHub/planetoftheweb/sassEssentials

[Sass Docs](https://sass-lang.com/documentation)

Sass is a css extnetion that adds functionality to stylesheets. it is a preprocessed language (must be translated - into vanilla css - before browser can read it )4.html

Sass Features:

- variables
- nesting
- partials
- extend
- operators
- mixins

using `.scss` files maintains the regualr css syntax

using **gulp** (consider exploring webpack)

## automation template

```bash
➜  planetoftheweb git clone https://github.com/planetoftheweb/sassEssentials.git
➜  sassEssentials git:(master) ✗ npm install
➜  sassEssentials git:(master) ✗ sudo npm install -g gulp
➜  sassEssentials git:(master) ✗ gulp
```

## project structure

use an underscore at the beginning of file name to indicate that the file will be imported (not processed)

```
├── builds
├── gulpfile.js
├── hero.png
├── node_modules
├── package.json
├── package-lock.json
├── process
    └── sass
        ├── _base.scss
        ├── _interface.scss
        ├── _mixins.scss
        ├── modules
            ├── _backgrounds.scss
            ├── _media.scss
            ├── _navigation.scss
            └── _tables.scss
        ├── _normalize.scss
        ├── style.scss
        └── _variables.scss
└── README.md
```

```scss
/* style.scss*/
@import "variables";
@import "normalize";
@import "mixins";
@import "base";
@import "interface";

@import "modules/backgrounds";
@import "modules/media";
@import "modules/tables";
@import "modules/navigation";
```

## variables

## mixin

```scss
/*_mixins.scss*/
@mixin backImage($image, $height: 100vh, $bgPos: center center) {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.6)),
    url($image);
  background-repeat: no-repeat;
  background-position: $bgPos;
  background-size: cover;
  height: $height;
}
```

```scss
/*_backgrounds.scss*/
.jumbotron {
  @include backImage("../images/water.jpg", 600px);
  margin-top: 0;
}
```

## invisible class & extend

```scss
/*_interface.scss*/
/* invisible class - "%" */
%btn {
  display: inline-block;
  padding: 6px 12px;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  cursor: pointer;
  border: none;
  border-radius: 4px;
  font-family: $font-highlight;
  user-select: none;
  color: $color-btn-text;
}

$color-btns: (
  default: $color-main,
  hot: $red,
  cool: $blue,
  awesome: $purple,
);

@each $key, $value in $color-btns {
  .btn-#{$key} {
    @extend %btn;
    background-color: $value;
  }
}
```
