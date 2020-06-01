# SCSS Utils Collection

## Install

```
npm install @wide/styles-utils --save
```

## Usage

- [a11y](#a11y)
- [breakpoint](#breakpoint)
- [button](#button)
- [element](#element)
- [font](#font)
- [grid](#grid)
- [list](#list)
- [pseudo-classs](#pseudo-classs)
- [text](#text)
- [touch](#touch)


<br/>

## a11y

- [only()](#a11y-only)
- [focusable()](#a11y-focusable)

### <a name="a11y-only"></a>`only()`

Applies accessible hiding to the current element.

```scss
@use '@wide/styles-utils' as mixins;

/* With `!important` property */
.a11y {
    @include mixins.a11y-only();
}

/* Without `!important` property */
.a11y-not-important {
    @include mixins.a11y-only(false);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Boolean` | Whether the visibility is important | `false` | `true` |

#### Output
```css
/* With `!important` property */
.a11y {
    border: 0 !important;
    clip: rect(0 0 0 0) !important;
    height: 1px !important;
    margin: 0 !important;
    overflow: hidden !important;
    padding: 0 !important;
    position: absolute !important;
    white-space: nowrap !important;
    width: 1px !important;
}
```

### <a name="a11y-focusable"></a>`focusable()`

Allows an accessibly hidden element to be focusable via keyboard navigation.

```scss
@use '@wide/styles-utils' as mixins;

/* With `!important` property */
.a11y-focusable {
    @include mixins.a11y-focusable();
}

/* Without `!important` property */
.a11y-focusable-not-important {
    @include mixins.a11y-focusable(false);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Boolean` | Whether the visibility is important | `false` | `true` |

#### Output
```css
/* With `!important` property */
.a11y-focusable:not(:focus) {
    border: 0 !important;
    clip: rect(0 0 0 0) !important;
    height: 1px !important;
    margin: 0 !important;
    overflow: hidden !important;
    padding: 0 !important;
    position: absolute !important;
    white-space: nowrap !important;
    width: 1px !important;
}
```

<br/>


## breakpoint

- [up()](#breakpoint-up)
- [down()](#breakpoint-down)
- [between()](#breakpoint-between)
- [only()](#breakpoint-only)
- [print()](#breakpoint-print)

### <a name="breakpoint-up"></a>`up()`

Define a media query value as the minimun reaching point.

```scss
@use '@wide/styles-utils' as mixins;

.show-from-sm {
    @include mixins.bp-up(sm) {
        color: green;
    }

    @include mixins.bp-up(sm, true) {
        color: fuchsia;
    }
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String\|Number` | The min media query value (xs, 1500px, 30em, ...) | `true` |  |
| `Boolean` | Is the media query measurement is `height` ? | `false` | `false` |
| `String` | The media query type (all, screen, ...) | `false` | `all` |

#### Output
```css
@media (min-width: 36em) {
    .show-from-sm {
        color: green;
    }
}

@media (min-height: 36em) {
    .show-from-sm {
        color: fuchsia;
    }
}
```

### <a name="breakpoint-down"></a>`down()`

Define a media query value as the maximum reaching point.

```scss
@use '@wide/styles-utils' as mixins;

.show-until-lg {
    @include mixins.bp-down(lg) {
        color: blue;
    }

    @include mixins.bp-lg(lg, true) {
        color: red;
    }
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String\|Number` | The max media query value (xs, 1500px, 30em, ...) | `true` |  |
| `Boolean` | Is the media query measurement is `height` ? | `false` | `false` |
| `String` | The media query type (all, screen, ...) | `false` | `all` |

#### Output
```css
@media (max-width: 63.99875em) {
    .show-until-lg {
        color: blue;
    }
}

@media (min-height: 63.99875em) {
    .show-until-lg {
        color: red;
    }
}
```

### <a name="breakpoint-between"></a>`between()`

Define a range of media query values.

```scss
@use '@wide/styles-utils' as mixins;

.show-between {
    @include mixins.bp-between(sm, md) {
        color: orange;
    }

    @include mixins.bp-between(sm, md, true) {
        color: purple;
    }

    @include mixins.bp-between(sm, 1500) {
        color: gold;
    }
    @include mixins.bp-between(1500, sm) {
        color: yellow;
    }
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String\|Number` | The min media query value (xs, 1500px, 30em, ...) | `true` |  |
| `String\|Number` | The max media query value (xs, 1500px, 30em, ...) | `true` |  |
| `Boolean` | Is the media query measurement is `height` ? | `false` | `false` |
| `String` | The media query type (all, screen, ...) | `false` | `all` |

> **Note**  
> There is a security method which test the both values and sort them from the lowest to the highest

#### Output
```css
@media (min-width: 36em) and (max-width: 48em) {
  .show-between {
    color: orange;
  }
}

@media (min-height: 36em) and (max-height: 48em) {
  .show-between {
    color: purple;
  }
}

@media (min-width: 36em) and (max-width: 93.75em) {
  .show-between {
    color: gold;
  }
}
@media (min-width: 36em) and (max-width: 93.75em) {
  .show-between {
    color: yellow;
  }
}
```

### <a name="breakpoint-only"></a>`only()`

Define a media query value as the only reaching point.

```scss
@use '@wide/styles-utils' as mixins;

.show-only {
    @include mixins.bp-only(xl) {
        color: indigo;
    }

    @include mixins.bp-only(xxl) {
        color: brown;
    }
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String\|Number` | The media query value (xs, 1500px, 30em, ...) | `true` |  |
| `String` | The media query type (all, screen, ...) | `false` | `all` |

#### Output
```css
@media (min-width: 75em) and (max-width: 99.99875em) {
  .test {
    color: indigo;
  }
}

@media (min-width: 100em) {
  .test {
    color: brown;
  }
}
```

### <a name="breakpoint-print"></a>`print()`

Define print media query rules.

```scss
@use '@wide/styles-utils' as mixins;

.print {
    @include mixin.bp-print() {
        color: beige;
    }
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String\|Number` | The media query value (xs, 1500px, 30em, ...) | `true` |  |
| `String` | The media query type (all, screen, ...) | `false` | `all` |

#### Output
```css
@media print {
    .print {
        color: beige;
    }
}
```

<br/>

## button

- [reset()](#button-reset)

### <a name="button-reset"></a>`reset()`

Reset button state to normal element.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.btn-reset();
    /* new rules here */
}
```

#### Output
```css
.btn {
    background: transparent;
    border: 0;
    padding: 0;
    /* new rules here */
}
```

<br/>

## element

- [clearfix()](#element-clearfix)
- [centerer()](#element-centerer)
- [vcenter()](#element-vcenter)
- [ratio()](#element-ratio)
- [position()](#element-position)
- [trbl()](#element-trbl)

### <a name="element-clearfix"></a>`reset()`

Micro clearfix rules for containing floats.

```scss
@use '@wide/styles-utils' as mixins;

.clearfix {
    @include mixins.el-clearfix();
}
```

#### Output
```css
.clearfix::after {
    clear: both;
    content: '';
    display: block;
}
```

### <a name="element-centerer"></a>`centerer()`

Center an element on the horizontal and vertical axis in absolute position.

```scss
@use '@wide/styles-utils' as mixins;

.center-horizontal {
    @include mixins.el-centerer(true, false);
}

.center-vertical {
    @include mixins.el-centerer(false);
}

.center-h-v {
    @include mixins.el-centerer();
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Boolean` | Horizontal centering | `false` | `true` |
| `Boolean` | Vertical centering | `false` | `true` |

#### Output
```css
.center-horizontal {
    position: absolute;
    left: 50%;
    transform: translate(-50%, 0);
}

.center-vertical {
    position: absolute;
    top: 50%;
    transform: translate(0, -50%);
}

.center-h-v {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}
```

### <a name="element-vcenter"></a>`vcenter()`

Vertically-center the direct descendants of the current element.  

Centering is achieved by displaying children as inline-blocks. Any whitespace between elements is nullified by redefining the font size of the container and its children.

```scss
@use '@wide/styles-utils' as mixins;

.v-center {
    @include mixins.el-vcenter();
}
```

#### Output
```css
.v-center {
    font-size: 0;
}
.v-center::before {
    content: '';
    display: inline-block;
    height: 100%;
    vertical-align: middle;
}
.v-center > * {
    display: inline-block;
    font-size: 1rem;
    vertical-align: middle;
}
```

### <a name="element-ratio"></a>`ratio()`

Lock the aspect ratio of an element – or make it fit to content if it exceeds the boundaries of the aspect ratio.

Note! the ratio is produced using the :before and :after pseudo-elements.  
Why it won't work on empty tags like `<img />`, `<input />` etc.

If used with flexbox – the ratio keeping pesudo element will actas a hidden flex-item.

```scss
@use '@wide/styles-utils' as mixins;

.ratio {
    @include mixins.el-ratio();
}

.ratio-16-9 {
    @include mixins.el-ratio(16, 9);
}

.ratio-custom {
    @include mixins.el-ratio(1.777778);
}

.ratio-width-height {
    @include mixins.el-ratio(4px, 3px);
}

.ratio-custom-keyword {
    @include mixins.el-ratio($ratio: 1.2);
}
```

#### Parameters
Possibility to handle one or two arguments: `ratio` or `width`, `height`

If one argument:

| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number\|Any` | Ratio value. Could be define as `1.2` or by keyword `$ratio: 1.2` | `false` | 1:1 |

If two arguments:

| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | Width value | `true` | |
| `Number` | Height value | `true` | |

#### Output
```css
.ratio::before,
.ratio::after {
    content: "";
    clear: both;
    display: table;
    margin-left: -1px;
    width: 1px;
}
.ratio::before {
    float: left;
    padding-bottom: 100%;
}

.ratio-16-9::before,
.ratio-16-9::after {
    content: "";
    clear: both;
    display: table;
    margin-left: -1px;
    width: 1px;
}
.ratio-16-9::before {
    float: left;
    padding-bottom: 56.25%;
}

.ratio-custom::before,
.ratio-custom::after {
    content: "";
    clear: both;
    display: table;
    margin-left: -1px;
    width: 1px;
}
.ratio-custom::before {
    float: left;
    padding-bottom: 56.2499929688%;
}

.ratio-width-height::before,
.ratio-width-height::after {
    content: "";
    clear: both;
    display: table;
    margin-left: -1px;
    width: 1px;
}
.ratio-width-height::before {
    float: left;
    padding-bottom: 75%;
}

.ratio-custom-keyword::before,
.ratio-custom-keyword::after {
    content: "";
    clear: both;
    display: table;
    margin-left: -1px;
    width: 1px;
}
.ratio-custom-keyword::before {
    float: left;
    padding-bottom: 83.3333333333%;
}
```


### <a name="element-position"></a>`position()`

Set position of an element using the syntax "padding-shorthand-syntax".

```scss
@use '@wide/styles-utils' as mixins;

.position {
    @include mixins.el-position();
}
.position-abs-10 {
    @include mixins.el-position(absolute, 10px);
}
.position-abs-10-20 {
    @include mixins.el-position(absolute, 10px, 20px);
}
.position-abs-10-20-30 {
    @include mixins.el-position(absolute, 10px, 20px, 30px);
}
.position-abs-10-20-30-40 {
    @include mixins.el-position(absolute, 10px, 20px, 30px, 40px);
}
.position-abs-0-0-30 {
    @include mixins.el-position($bottom: 30px);
}
.position-abs-10-10-30 {
    @include mixins.el-position(absolute, 10px, $bottom: 30px);
}
.position-abs-10--456 {
    @include mixins.el-position(absolute, 10px, $z-index: 456);
}
```

#### Parameters
Possibility to handle arguments by keywords: `position`, `top`, `right`, `bottom`, `left` and `z-index`.

| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String` | Position | `false` | `absolute` |
| `Number` | Top | `false` | `0` |
| `Number` | Right | `false` | `0` |
| `Number` | Bottom | `false` | `0` |
| `Number` | Left | `false` | `0` |
| `Number\|String` | z-index | `false` | `auto` |

#### Output
```css
.position {
    bottom: 0;
    left: 0;
    position: absolute;
    right: 0;
    top: 0;
    z-index: auto;
}

.position-abs-10 {
    bottom: 10px;
    left: 10px;
    position: absolute;
    right: 10px;
    top: 10px;
    z-index: auto;
}

.position-abs-10-20 {
    bottom: 10px;
    left: 20px;
    position: absolute;
    right: 20px;
    top: 10px;
    z-index: auto;
}

.position-abs-10-20-30 {
    bottom: 30px;
    left: 20px;
    position: absolute;
    right: 20px;
    top: 10px;
    z-index: auto;
}

.position-abs-10-20-30-40 {
    bottom: 30px;
    left: 40px;
    position: absolute;
    right: 20px;
    top: 10px;
    z-index: auto;
}

.position-abs-0-0-30 {
    bottom: 30px;
    left: 0;
    position: absolute;
    right: 0;
    top: 0;
    z-index: auto;
}

.position-abs-10-10-30 {
    bottom: 30px;
    left: 10px;
    position: absolute;
    right: 10px;
    top: 10px;
    z-index: auto;
}

.position-abs-10--456 {
    bottom: 10px;
    left: 10px;
    position: absolute;
    right: 10px;
    top: 10px;
    z-index: 456;
}
```

### <a name="element-trbl"></a>`trbl()`

Set edges properties of an element to a unit above/below using a "padding-shorthand-syntax" (top, right-left, bottom)... and it takes keywords too.

```scss
@use '@wide/styles-utils' as mixins;

.trbl {
    @include mixins.el-trbl();
}
.trbl-10 {
    @include mixins.el-trbl(10px);
}
.trbl-10-20 {
    @include mixins.el-trbl(10px, 20px);
}
.trbl-10-20-30 {
    @include mixins.el-trbl(10px, 20px, 30px);
}
.trbl-10-20-30-40 {
    @include mixins.el-trbl(10px, 20px, 30px, 40px);
}
.trbl-0-0-30 {
    @include mixins.el-trbl($bottom: 30px);
}
.trbl-10-10-30 {
    @include mixins.el-trbl(10px, $bottom: 30px);
}
```

#### Parameters
Possibility to handle arguments by keywords: `top`, `right`, `bottom` and `left`.

| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | Top | `false` | `0` |
| `Number` | Right | `false` | `0` |
| `Number` | Bottom | `false` | `0` |
| `Number` | Left | `false` | `0` |

#### Output
```css
.trbl {
    bottom: 0;
    left: 0;
    right: 0;
    top: 0;
}

.trbl-10 {
    bottom: 10px;
    left: 10px;
    right: 10px;
    top: 10px;
}

.trbl-10-20 {
    bottom: 10px;
    left: 20px;
    right: 20px;
    top: 10px;
}

.trbl-10-20-30 {
    bottom: 30px;
    left: 20px;
    right: 20px;
    top: 10px;
}

.trbl-10-20-30-40 {
    bottom: 30px;
    left: 40px;
    right: 20px;
    top: 10px;
}

.trbl-0-0-30 {
    bottom: 30px;
    left: 0;
    right: 0;
    top: 0;
}

.trbl-10-10-30 {
    bottom: 30px;
    left: 10px;
    right: 10px;
    top: 10px;
}
```

<br/>



## font

- [face()](#font-face)
- [size()](#font-size)

### <a name="font-face"></a>`face()`

Generates an `@font-face` declaration.

You can choose the specific file formats you need to output; the mixin supports `eot`, `ttf`, `svg`, `woff2` and `woff`.

```scss
@use '@wide/styles-utils' as mixins;

@include mixins.font-face(
    "source-sans-pro",
    "fonts/source-sans-pro-regular",
    ("woff2", "woff")
) {
    font-style: normal;
    font-weight: 400;
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `String` | The font family name | `true` | |
| `String` | The path to the font family | `true` | |
| `String\|List` | A list of file formats to support | `false` | `("ttf", "woff2", "woff")` |

#### Output
```css
@font-face {
    font-family: "source-sans-pro";
    src: url("fonts/source-sans-pro-regular.woff2") format("woff2"), url("fonts/source-sans-pro-regular.woff") format("woff");
    font-style: normal;
    font-weight: 400;
}
```

### <a name="font-size"></a>`size()`

Generate a font-size and baseline-compatible line-height.

```scss
@use '@wide/styles-utils' as mixins;

.font-12 {
    @include mixins.font-size(12);
}

.font-12-20-i {
    @include mixins.font-size(12, 20, true);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | The size of the font | `true` | |
| `Number\|String` | The line box height | `false` | `auto` |
| `Boolean` | Whether the font-size is important | `false` | `false` |

#### Output
```css
.font-12 {
    font-size: 0.75em;
    line-height: 1.05;
}

.font-12-20-i {
    font-size: 0.75em !important;
    line-height: 1.25em !important;
}
```

<br/>

## grid

- [container()](#grid-container)
- [size()](#grid-item)

### <a name="grid-container"></a>`container()`

Generate the grid container.  
It uses the [negative margin trick](http://csswizardry.com/2011/08/building-better-grid-systems/) for multi-row grids.

```scss
@use '@wide/styles-utils' as mixins;

.container {
    @include mixins.grid-container();
}

.container-gutter-10 {
    @include mixins.grid-container(10px, false);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | The size if the gutters | `false` | `0` |
| `Boolean` | Define if the whitespace fix is enable | `false` | `true` |

#### Output
```css
.container {
    margin: 0;
    padding: 0;
    list-style: none;
    font-size: 0;
    margin-left: 0;
}

.container-gutter-10 {
    margin: 0;
    padding: 0;
    list-style: none;
    margin-left: -10;
}
```

### <a name="grid-item"></a>`item()`

Generate the grid item.

1. Required in order to combine fluid widths with fixed gutters.
2. Allows us to manipulate grids vertically, with text-level properties, etc.
3. Default item alignment is with the tops of each other, like most traditional grid/layout systems.
4. By default, all layout items are full-width (mobile first).
5. [Gutters provided by left padding](http://csswizardry.com/2011/08/building-better-grid-systems/)

```scss
@use '@wide/styles-utils' as mixins;

.grid-item {
    @include mixins.grid-item();
}

.grid-item-gutter-10 {
    @include mixins.grid-item(10px, false);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | The size if the gutters | `false` | `0` |
| `Boolean` | Define if the whitespace fix is enable | `false` | `true` |

#### Output
```css
.grid-item {
    box-sizing: border-box;
    display: inline-block;
    vertical-align: top;
    width: 100%;
    font-size: 1rem;
    padding-left: 0;
}

.grid-item-gutter-10 {
    box-sizing: border-box;
    display: inline-block;
    vertical-align: top;
    width: 100%;
    padding-left: 10px;
}
```

<br/>

## list

- [reset()](#list-reset)

### <a name="list-reset"></a>`reset()`

Injects generic rules for disabling `ul`, `ol`, `li` styles.

```scss
@use '@wide/styles-utils' as mixins;

.list {
    @include mixins.list-reset();
}
```

#### Output
```css
.list {
    list-style: none;
    margin: 0;
    padding: 0;
}
```

<br/>

## pseudo-classs

- [a()](#pc-a)
- [af()](#pc-af)
- [ah()](#pc-ah)
- [afh()](#pc-afh)
- [f()](#pc-f)
- [fh()](#pc-fh)
- [h()](#pc-h)

### <a name="pc-a"></a>`a()`

Generate `:active` style in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-a() {
        background-color: red;
    }
}
```

#### Output
```css
.btn:active {
    background-color: red;
}
```

### <a name="pc-af"></a>`af()`

Generate `:active` and `:focus` styles in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-af() {
        background-color: blue;
    }
}
```

#### Output
```css
.btn:active,
.btn:focus {
    background-color: blue;
}
```

### <a name="pc-ah"></a>`ah()`

Generate `:active` and `:hover` styles in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-ah() {
        background-color: green;
    }
}
```

#### Output
```css
.btn:active,
.btn:hover {
    background-color: green;
}
```

### <a name="pc-afh"></a>`afh()`

Generate `:active`, `:focus` and `:hover` styles in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-afh() {
        background-color: yellow;
    }
}
```

#### Output
```css
.btn:active,
.btn:focus,
.btn:hover {
    background-color: yellow;
}
```

### <a name="pc-f"></a>`f()`

Generate `:focus` style in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-f() {
        background-color: cyan;
    }
}
```

#### Output
```css
.btn:focus {
    background-color: cyan;
}
```

### <a name="pc-fh"></a>`fh()`

Generate `:focus` and `:hover` styles in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-fh() {
        background-color: black;
    }
}
```

#### Output
```css
.btn:focus,
.btn:hover {
    background-color: black;
}
```

### <a name="pc-h"></a>`h()`

Generate `:hover` styles in one go.

```scss
@use '@wide/styles-utils' as mixins;

.btn {
    @include mixins.pc-h() {
        background-color: white;
    }
}
```

#### Output
```css
.btn:hover {
    background-color: white;
}
```

<br/>

## text

- [truncate()](#text-truncate)

### <a name="text-truncate"></a>`truncate()`

Prevent text from wrapping onto multiple lines for the current element.  
An ellipsis is appended to the end of the line.

```scss
@use '@wide/styles-utils' as mixins;

.text-truncated {
    @include mixins.text-truncate();
}

.text-truncated-50px {
    @include mixins.text-truncate(50px);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Number` | The maximum width of element | `false` | `100%` |

#### Output
```css
.text-truncated {
    max-width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.text-truncated-50px {
    max-width: 50px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
```

<br/>

## touch

- [scroll()](#touch-scroll)
- [tap()](#touch-tap)
- [enabled()](#touch-enabled)
- [disabled()](#touch-disabled)

### <a name="touch-scroll"></a>`scroll()`

Set whether or not touch devices use momentum-based scrolling for the given element.  
By default, applies momentum-based scrolling for the current element.

```scss
@use '@wide/styles-utils' as mixins;

.touch-scroll {
    @include mixins.touch-scroll();
}
```

#### Output
```css
.touch-scroll {
    -webkit-overflow-scrolling: touch;
}
```

### <a name="touch-tap"></a>`tap()`

Set the color of the highlight that appears over a link while it's being tapped.  
By default, the highlight is suppressed.

```scss
@use '@wide/styles-utils' as mixins;

.touch-scroll {
    @include mixins.touch-tap();
}

.touch-scroll-red {
    @include mixins.touch-tap(red);
}
```

#### Parameters
| Type | Description | Mandatory | Default |
|---|---|---|---|
| `Color` | The value of the highlight | `false` | `rgba(0, 0, 0, 0)` |

#### Output
```css
.touch-scroll {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}

.touch-scroll-red {
    -webkit-tap-highlight-color: red;
}
```

### <a name="touch-enabled"></a>`enabled()`

Finding out if touch is available for the page document.

```scss
@use '@wide/styles-utils' as mixins;

.text-size-mobile {
    @include mixins.touch-enabled() {
        font-size: 1.2rem;
    }
}
```

#### Output
```css
.-touch-based .text-size-mobile {
    font-size: 1.2rem;
}
```

### <a name="touch-disabled"></a>`disabled()`

Finding out if touch is not available for the page document.

```scss
@use '@wide/styles-utils' as mixins;

.text-size {
    @include mixins.touch-disabled() {
        font-size: 1rem;
    }
}
```

#### Output
```css
:not(.-touch-based) .text-size {
    font-size: 1rem;
}
```

<br />
<br />

## Authors

- **Aymeric Assier** - [github.com/myeti](https://github.com/myeti)
- **Julien Martins Da Costa** - [github.com/jdacosta](https://github.com/jdacosta)

<br />

### Contributors

- **Sébastien Robillard** - [github.com/robiseb](https://github.com/robiseb)

<br />
<br />

## Resources 
- [Locomotive boilerplate](https://github.com/locomotivemtl/locomotive-boilerplate)

<br />
<br />

## License

This project is licensed under the MIT License - see the [licence](licence) file for details