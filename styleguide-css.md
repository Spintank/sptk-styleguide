# sptk-styleguide-css
*The CSS coding styleguide of Spintank*

## Table of contents
1. [Introduction](#introduction)
    - [Formating](#formating)
    - [Comments](#comments)
    - [OOCSS and BEM](#oocss-and-bem)
    - [Units](#units)
2. [CSS](#css)
    - [Selectors](#selectors)
    - [Properties](#properties)
        - [Ordering of property declarations](#ordering-of-property-declarations)
    - [Practices](#practices)
        - [Titles and paragraphs](#titles-and-paragraphs)
    - [Tips](#tips)
        - [Position](#position)
        - [Border](#border)
3. [SASS](#sass)
   - [Syntax](#syntax)
   - [Ordering of sass property declarations](#ordering-of-sass-property-declarations)
        - [Variables](#variables)
        - [Mixins](#mixins)
   - [Nested](#nested)
   - [DRY](#dry)
   - [Mobile first](#mobile-first)


## Introduction

There some informations about our Css coding practices.

### Formating

* Use soft tabs (2 spaces) for indentation
* Use dashes over camelCasing in class names, **reserve camelCasing for ID**.
* Do not use ID selectors ([level1](https://developer.mozilla.org/fr/Apprendre/CSS/Les_bases/La_cascade_et_l_h%C3%A9ritage))
* Do not use !important
* When using multiple selectors in a rule declaration, give each selector its own line.
* Put a space before the opening brace `{` in rule declarations
* In properties, put a space after, but not before, the `:` character.
* Put closing braces `}` of rule declarations on a new line
* Put blank lines between rule declarations

```css
.myselector {
  border: 0;
}

.myselector,
.myotherselector {
  border: 0;
}
```

### Comments

* Use comments to explain and clarify your code

* Use this style to comment your **section**

```css
////////
////
//// Header
////
///////
```

* Use this style to comment your **subsection**

```css
/* Navigation */
.nav {
  // ...
}
```

* Use this style to comment your **line**

```css
.nav {
  z-index : 0; // To do something  
}
```

### OOCSS and BEM

We encourage some combination of [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/)(Object Oriented CSS) and [BEM](https://css-tricks.com/bem-101/)(Block-Element-Modifier) for these reasons:

- It helps create clear, strict relationships between CSS and HTML
- It helps us create reusable, composable components
- It allows for less nesting and lower specificity
- It helps in building scalable stylesheets

In Spintank we use a kind of BEM like this :

```css
/* Example */
.myclass { }
.myclass_block { }
.myclass_block--modifier { }

/* List Card */
.cardlist { }
.cardlist_item { }
.cardlist_item--big { }
```

```html
<ul class="cardlist">
    <li class="cardlist_item">
        <!-- ... -->
    </li>
    <li class="cardlist_item cardlist_item--big">
        <!-- ... -->
    </li>
    <li class="cardlist_item">
        <!-- ... -->
    </li>
</ul>
```

Avoid to have longer class, think about this, maybe you must create another block :


```html
<!--BAD-->
<ul class="cardlist">
    <li class="cardlist_item">
        <div class="cardlist_item_content">
            <h3 class="cardlist_item_content_title">Foo</h3> <!--Too long no ?-->
            <!-- ... -->
        </div>
    </li>
</ul>


<!--GOOD-->
<ul class="cardlist">
    <li class="cardlist_item card"> <!-- .card has common properties of all cards // .cardlist_item has layout properties -->
        <div class="card_content">
            <h3 class="card_title">Bar</h3>
            <!-- ... -->
        </div>
    </li>
</ul>
```


### Units

- Use REM or EM units instead of px : usually we use REM unit :

```css

/* base.scss */
html {
  font-size: 62.5%; // 10px = 1rem;
}

/* foo.scss */
.bar {
  padding-top: 3rem; // 30px
}

```

## CSS

### Selectors

- Selectors are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes.
- Do not target HTML tags directly, better use .class to apply styles. Then you can change html tag can and keep same style, it force you to write reusable CSS code (OOCSS).

```css

/* BAD */
h2 {
  font-size: 13px;
}

/* GOOD */
.title-beta {
  font-size: 13px;
}

```

```html
<h2 class="title-beta">Foo</h2>
```

### Properties

- Properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations

#### Ordering of property declarations

Try to keep order in your property declarations

1.Positioning
```css
.foo {
  display: block;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 1;
  float: left;
  clear: both;
  // ...
}
```
2.Dimension
```css
.foo {
  // ...
  width: 10rem;
  height: 10rem;
  min-width: 5rem;
  max-width: 15rem;
  min-height: 5rem;
  max-height: 15rem;
  // ...
}
```
3.Margins
```css
.foo {
  // ...
  margin: 0 auto;
  padding: 3rem;
  border: 2px solid $theme-color;
  // ...
}
```
4.Text
```css
.foo {
  // ...
  font-family: "Arial", sans-serif;
  font-weight: 400;
  font-size: 12px;
  line-height: 1.5;
  text-align: center;
  text-indent: 30px;
  text-decoration: none;
  text-transform: uppercase;
  color: $text-color;
  // ...
}
```
5.Background
```css
.foo {
  // ...
  background-color: $theme-color;
  background-image: url('..');
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  // ...
}
```
6.Animations
```css
.foo {
  // ...
  transition: transform 1s ease;
  // ...
}
```

### Practices

#### Titles and paragraphs

- When you start your project, try to list styles of titles and paragraphs to make generic classes. Then it's easy to change fonts styles with one class.

```css
/* Examples */

.title--alpha{
  font-size: 20px;
  //...
}

.paragraph--alpha{
  font-size: 10px;
  //...
}
```

```html
<div class="card">
    <h2 class="card_title title--alpha">Foo</h2> <!-- .card_title has margins properties // .title--alpha has font styles properties -->
</div>
```

#### Tips

##### Position

- Do not use top / right / bottom / left properties with position relative. Use transform property.

```css
/* BAD */
.foo{
  position: relative;
  top: 2rem;
  left: 2rem;
}

/* Good */
.foo{
  position: relative;
  transform: translate(2rem, 2rem);
}
```

- If a value is set to 0, do not use px.

```css
/* BAD */
.foo{
  position: relative;
  top: 0px;
  left: 0px;
}

/* Good */
.foo{
  position: relative;
  top: 0;
  left: 0;
}
```

##### Border

- Do not use REM with border, better use px (IE problem)

```css
/* BAD */
.foo{
  border: 1rem solid $theme-color;
}

/* Good */
.foo{
  border: 10px solid $theme-color;
}
```

- Use 0 instead of none to specify that a style has no border.

```css
/* BAD */
.foo{
  border: none;
}

/* Good */
.foo{
  border: 0;
}
```

## SASS

###Syntax

Use the .scss syntax, never the original .sass syntax

### Ordering of sass property declarations

1.Property declarations

List all standard property declarations.

```scss
.cardlist {
  padding: 4rem 0;
  // ...
}
```

2.`@include` declarations

Put `@include`s at the end

```scss
.cardlist {
  padding: 4rem 0;
  //..
  @include stretch();
}
```

3.Nested selectors

   Nested selectors, _if necessary_, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

```scss
.cardlist {
  padding: 4rem 0;

  &_item{
    //..

    &:after{
      /..
    }
  }
}
```

### Nested


Do not nest selectors more than **three levels deep!**

```scss
.cardlist {
  .card {
    .card_title {
      // STOP!
    }
  }
}
```

### DRY

Don't repeat yourself ! Use Sass features like mixins and variables.

#### Variables
Prefer dash-cased variable names (e.g. `$my-variable`) over camelCased or snake_cased variable names.
Declare your variables in **config.scss**.

##### Colors Variables
```scss
/* config.scss */
$theme-color: #fff!default;
```

##### Fonts variables
```scss
/* config.scss */
$font-regular: 'Arial', sans-serif !default;
$font-bold: 'ArialBold', sans-serif !default;
```

#### Mixins

Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions.
Declar your mixins in **mixins.scss**



```scss
/* config.scss */
@mixin hide-for-viewer {
   position: absolute;
   height:  1px;
   width:   1px;
   padding: 0;
   border:  0;
   overflow: hidden;
   clip: rect(1px  1px  1px  1px);
}
```

### Mobile first

Display styles for mobile then tablet, then desktop... The order is very important, you must do mobile first. To do responsive css, use [sass_mq](http://sass-mq.github.io/sass-mq/).

1.Define your breakpoints
```scss
/* config.scss */
$mq-breakpoints: (
  mobile: 320px,
  tablet: 600px,
  desktop: 1024px,
  wide: 1400px,
);
```
2.Use the mixin
```scss
/* *.scss */
.title--alpha {
  font-size: 14px;

  @include mq($from: tablet) {
    font-size: 18px;
  }

  @include mq($from: desktop) {
    font-size: 20px;
  }
}
```

## THE END

**Made with love at Spintank &#9996;**
