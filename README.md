# Rules and principles for scalable CSS

## Necessity to comply with agreements

CSS (cascading style sheets) actually don't have a strict declaration and each developer can write CSS as he or she sees fit. This may work for a small project where the development team is one person. But for large, scalable projects that require support, best practice requires that teams follow a stricter discipline for writing CSS.

These are the benefits from having developers follow the same set of rules and principles:

1. Single solid style. All CSS files will look as if they were written by one person, even if there is a whole team of developers. 
2. The code will be transparent for all participants in the development process. A very minimal amount of time will be spent trying to understand the code.
3. Development productivity will increase. Strict rules shorten the time required for editing and creating new styles.
4. The code will be scalable and reusable.
5. New developers on the project can be quickly brought up to speed.

##Selector declaration

All selector declarations must conform to the following pattern:

```css
selector,
selector {
    property: value;
    property: value;
}
```

1. If a declaration specifies multiple selectors, each of them must begin on a new line.
2. Indentation from the left margin should be 4 whitespaces. Whitespaces shouldn't be mixed with Tabs.
3. The opening curly brace ({) should be separated from the selector by a single space and is located on one line with the last selector.
4. Property and Value must be written on one line.
5. The Value should separated from the colon (:) by a single space.
6. The description of each property ends with a semicolon (;).
7. The closing curly brace (}) is always placed on a new line with no indentation from the edge.
8. Omit the '0' before '.' for non-integer values ​​from -1 to 1 (where it is possible).
9. Use a hex notation for colors and shorthand hex where it is possible (for example, #aaa). If you use rgba notation then it needs to start with a callback in hex (for browsers which do not support rgba).
10. Property '!important' should be avoided. This is permissible only as a last resort as a temporary solution to urgent problems. The property that includes '!important' should always be accompanied with the reason for the comment.
11. Use only single quotes in the declaration of properties.
12. Do not put quotes inside a 'url()'.
13. Use lowercase for selectors and properties (exception: names like "font-family").

```css
.product__note {
    font-family: 'Times New Roman', Times, Georgia, sans-serif;
    font-size: .9em;
    font-style: italic !important; /* reason for !important */
    line-height: 1.45;

    backgroung: url(../i/pic_bg.jpg) no-repeat 0 0 transparent;
    color: #aaa; /* callback in hex */
    color: rgba(170, 170, 170, .9);
}
```
_Exception:_ selector with only one property should be written on one line:

```css
selector { property: value; }
```

```css
.product__title { font-weight: bold; }
```

## Naming convention

For the name of the selectors we adhere to the BEM ideology. BEM is a methodology and set of tools for front-end development created by Yandex. We will take only a part of the methodology - the naming of CSS selectors.

### Short introduction to BEM

_Block_ - absolutely independent entity, brick of a project. This unit can be simple or composite, i.e. contain other Blocks.

_Element_ - part of the Block, responsible for a particular function. It may be only a part of the Block and does not make sense in isolation from Block.

_Modifier_ - property of a Block (or Element) that changes the appearance or behavior. Has a name and a value. Several different Modifiers can be used simultaneously for one Block (or Element).

### Syntax
##### Block
If the name of the Block consists of several words, they are separated with a hyphen (-).

```css
.menu {
}

.product-categories {
}

```

##### Element
Elements consist of the Block's name, double underscore (__) and the name of the Element. For a composite Element's name you can use a hyphen (-).

```css
/**
 * 'menu__item', 'menu__promo-link' - Elements of the Block 'menu'
 */

.menu__item {
}

.menu__promo-link {
}
```

##### Modifier 
Modifiers consist of a Block's (or Element) name, a double hyphen (--), Modifier's name, underscore (_), and the Modifier's value.

```css
/**
 * 'menu--theme_categories' - Modifier for the Block 'menu'
 * 'theme' - Modifier name
 * 'categories' - Modifier value
 */

.menu--theme_categories {
}


/**
 * 'menu__item--type_promo' - Modifier for the Element 'menu__item'
 * 'type' - Modifier name
 * 'promo' - Modifier value
 */

.menu__item--type_promo {
}
```

#### Important features

* BEM-methodology excludes the use of id-type selectors for describing the styles (to avoid high specificity and to provide the possibility of re-using a Block). Only class-type selectors are allowed for style declaration.
* Selector names shouldn't be too abstract and at the same time shouldn't describe the content (for example, instead of '.red' it would be better to use '.title-error').
* The name of the class should be as short as possible, but at the same time it must be long enough to make sense.
* The names of Blocks, Elements and Modifiers should reflect as clearly as possible the meaning of the described unit.
* Selectors must not include html tags because we want to get context-independent style units.
* Cascading selectors should be excluded from CSS. Cascading is possible only in one case - between Modifier and Element.

Example of cascading:

```css
/**
 * 'menu--theme_categories' - Modifier for the Block 'menu'
 * 'menu__item' - Element for the Block 'menu'
 */

.menu--theme_categories .menu__item {
}
```

You can find more information about BEM here: <http://bem.info>


## Order of selector properties

To increase productivity of working with code, it is important to have the same order of describing the properties. All style properties are divided into 4 types: Position, Display & Box model, Typography and Other decoration styles.

Example:

```css
.current-list {
    /* Positioning */
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;

    /* Display & Box model */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 1px solid #333;
    margin: 0;    

    /* Typography */
    font-family: Arial, Tahoma, Verdana, sans-serif;
    font-size: 1.2em;
    text-align: left;
    line-height: 1.4;
    word-wrap: break-word;

	/* Other decoration styles */
    background-color: #fff;
    color: #333;
}
```

## Multiple CSS files

Each Block is described in a separate file and there is only one file which describes one Block. Files for Blocks also include Elements and Modifiers of Blocks. The name of the file must equal the Block name (for example, menu.css, product.css).

Global styles should be presented in separated CSS files (basic.css).


## Comments 

CSS files for each Block must begin with a title comment.

```css
/*------------------------------------*\
    
    #BLOCK-NAME

    Description: description of the block.
    
    Elements:
    ...
    
    Modifiers:
    ...

    HTML sample:
    <div class="...">
    	...
    </div>

\*------------------------------------*/
```

Comments for selectors:

```css
/**
 * Some comment
 */
```

TODO-comment for selector (developer's name is optional):

```css
/**
 * [@developer] TODO: some comment
 */
```

Each of selector's properties can have its own one-line explanatory comments:

```css
.btn--type_order {
    background-color: #ddd; /* TODO: replace color value by variable */
    text-decoration: none !important; /* preventing default behavior of '.a' */
}
```

## Line breaks

Line breaks in CSS are used for visual distinction. It’s recommended to use indentation and a line break between the declarations. When you need more visual differentiation, use 2 blank line breaks.

For example:

```css
/*------------------------------------*\
    
    #PRODUCT

    Description: displays detailed information about the product.
    
    Elements:
    product__picture
    product__title
    
    Modifiers:
    product--type_product-page
    product--type_grid
    
    HTML sample:
    <div class="menu menu--type-main">
    	<div class="menu__logo">
    	</div>
    </div>

\*------------------------------------*/

.product__picture {
	
}

.product__title {
	
}


/**
 * product--type_product-page - for detailed product page
 */

.product--type_product-page {
	
}

/**
 * product--type_product-page - for detailed product page
 */

.product--type_grid {
	
}
```

## Z-index

Which z-index value should be used depends on the context of use:

1. Page elements: 1-300.
2. Popup elements on a page: 101 - 300.
3. Modal windows: 301-600.
4. Popup elements in a modal windows: 601-900.

---

##Common rules for SASS

* Limit nesting level by one.
* Use ampersand (&) for BEM-style naming of a nested selectors
* Nested selectors should be indented from the left. 
* Nested selectors must be separated by one blank line above and below.

```scss
.ecard {
			
    &__header { /* ecar__header */
		
	}
	
}

.ecard--theme_confirmation {

    .ecard__title {
        font-weight: bold;
	}

}
```

All variables must be in a separate file (vars.scss)

To better support the CSS, variables must be defined for common properties, such as: font-size, font-family, line-height, color, background-color, min-width and max-width for @media. For example:

```scss
$font-size-s: 1.2em;
$font-size-m: 1.4em;
$font-size-l: 1.6em;

$line—height-s: 1.4;
$line—height-m: 1.6;
$line—height-l: 1.8;

$font-family-sans: 'Arial, Tahoma, Verdana, sans'; 
$font-family-serif: 'Times New Roman, Times, Georgia, sans-serif';

$color-text: #333;

$color-note: #999;

$color-link: #000;
$color-link-hover: #ff0000;

$min-width-s: 100;
$max-width-s: 100;

$min-width-m: 100;
$max-width-m: 100;

$min-width-l: 100;
$max-width-l: 100;

$min-width-xl: 100;
$max-width-xl: 100;

```

All global and basic styles should be placed in the basic.scss

---

## Common rules for responsive design

* All responsive pages should have a ‘viewport' meta-tag.
```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```
* Font size can be specified in '%', 'em' or 'rem' (with callbacks in 'em' for old browsers). You shouldn't specify the font size in fixed units like 'px' or 'pt'. *Exception:* 'pt' can only be used for the printed version of the page. 
* Do not specify a unit of measurement for the 'line-height’; ‘line-height' should be designed proportionally to the current font size.
```css
line-height: 1.4;
```
* Do not use \<table\> for layouts.
* For padding it is desirable to use em instead of px.
* Following the mobile-first rule, we should use only 'min-width' for media queries.
```css
@media all and (min-width: 50em) {...}
```

---

#Common rules for HTML

Preferable to use html5.

```html
<!DOCTYPE html>
```

In the tag \<link\> and \<script\> to reference the CSS and Javascript respectively, there is no need for the type attribute, it can be omitted.

```html
<!-- Not recommended -->
<link rel="stylesheet" href="//www.somedomain.com/css/style.css" type="text/css">
<script src="//www.somedomain.com/js/script.js" type="text/javascript"></script>
  
<!-- Recommended -->
<link rel="stylesheet" href="//www.somedomain.com/css/style.css">
<script src="//www.somedomain.com/js/script.js"></script>

```

Order of attributes in tags:

```html
<a class=""
   id=""
   role=“”
   data-name=""
   href=""
   title=“”>
   Text
</a>

<img class=""
     id=""
     src=""
     alt="">
```

Format of todo-comments (developer's name is optional):

```html
<!-- @asvyazhin TODO: remove optional tags -->
<!-- TODO: change <div> on <ul> -->
```

Layout should be semantic, tags should be associated with their purposes.

```html
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>

<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

All \<img\> should have an 'alt' attribute.

```html
<!-- Not recommended -->
<img src="product.png">

<!-- Recommended -->
<img src="product.png" alt="Product name">
```

## No self closing tags

With HTML5 we can omit the '/\>' for tags like \<br /\>, \<hr /\>, \<img /\> etc.

```html
<br>
<hr>
<img src=“”>
```

## Optional closing tags

In HTML5 (or non-XHTML syntax) we can omit closing tags from certain elements. But is recommended to use the closing tags so that the code will be clearer and will not confuse other team members.


```html
<!-- Not recommended -->
<ul>
    <li>
    <li>
</ul>

<!-- Recommended -->
<ul>
    <li></li>
    <li></li>
</ul>
```


## Line breaks

It is strongly recommended to separate semantic groups of tags by blank lines for the visual distinction.

```html
<dl>

    <dt>Lorem</dt>
    <dd>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</dt>

    <dt>Ipsum</dt>
    <dd>Vestibulum tortor quam, feugiat vitae, ultricies eget, tempor sit amet, ante.</dt>

    <dt>Dolor</dt>
    <dd>Morbi in sem quis dui placerat ornare. Pellentesque odio nisi euismod in pharetra.</dt>

</dl>
 
 
<div class="promo">

    <p><strong>Pellentesque habitant morbi tristique</strong> senectus et netus et malesuada fames ac turpis egestas.</p>    
    <a href="#" class="btn">Lorem</a>

</div>
```

## Comments on closing tags

After a long chain of tags that belong to the same semantic group, it is recommended to leave a comment after the last closing tag, for example:

```html
<div class="product">

    ...

    <div class="product__picture">
    ...
    </div><!-- /product__picture -->

    ...

</div><!-- /product -->
```

## Id and classes for Javascript

Id and class attributes are intended to work only with Javascript should not receive any decoration styles and always should be prefixed with 'js-'. For example:

```html
<div class="product js-product-collapsible">

    ...

</div>
```