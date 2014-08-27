# Rules and principles for the development of scalable CSS (Cascading style sheets).

## Necessity to comply with agreements

CSS-files do not have a strict declaration, each developer can make it as it sees fit. It may well work for a small project where the development team is one person. But for large, scalable and supported projects, we must follow by a strict discipline for writing cascading style sheets.

What are the benefits we get if all developers will follow the same set of rules and principles:

1. Single solid style. All CSS-files will look as if they were written by one person, even if there is a whole team of developers. 
2. The code will be transparent for all participants in the development process. On the understanding of the code will spents a minimum of time. 
3. Development productivity will increase. Strict rules to shorten the time required for editing and creating new styles.
4. The code will be scalable and reusable.
5. Easy entry to the project for new developers.

##Selector declaration

All selector declarations must conform to the following pattern:

```
[selector],
[selector] {
    [property]: [value];
    [property]: [value];
}
```

1. If a declaration specifying multiple selectors, each of them must begin on a new line.
2. The opening curly brace '{' should be separated from the selector by a single space and is located on one line with the last selector.
3. 'property' and 'value' must be written in one line.
4. 'value' is separated from the colon by a single space.
5. Description of each property ends with a semicolon.
6. The closing curly brace '}' is always placed on a new line with no indentation from the edge.
7. Indentation from the left margin equal to 4 whitespace. Whitespaces should not be mixed with tabs.
8. Omit the "0" for non-integer values ​​from -1 to 1, where it is possible (.9em).
9. Use a hex notation for colors. Shorthand hex where it is possible (#aaa).
10. Always use lowercase.
11. Use only single quotes in the declaration of properties.
12. Do not put quotes inside a tag 'url'.
13. Parameter '!important' should be avoided, this is permissible only as a last resort as a temporary solution of urgent problems. The property includes '!important' should always be accompanied TODO-comment.


```
WRONG
.product__note
{
    font-size: 0.9em;
    font-style: italic !important; /* Reason of important. TODO: remove !important */
    line-height: 1.45;

    backgroung: url('/i/pic_bg.jpg') no-repeat 0 0 transparent;
    color: #AAAAAA;
}
```

```
*** RIGHT ***
.product__note {
    font-size: .9em;
    font-style: italic !important; /* Reason of important. TODO: remove !important */
    line-height: 1.45;

    backgroung: url(/i/pic_bg.jpg) no-repeat 0 0 transparent;
    color: #aaa;
}
```
_Exception:_ selector only with one property should be written in one line:

```
[selector] { [property]: [value]; }
```

```
*** WRONG ***
.product_title {
    font-weight: bold;
}
```

```
*** RIGHT ***
.product_title { font-weight: bold; }
```

## Naming convention

In the name of the selectors we are adhere to the BEM ideology. BEM - a methodology and set of tools for User Interface development created by Yandex. We will take only a part of the methodology - the name of CSS selectors.

### Short introduction to BEM.

_Block_ - absolutely independent entity, brick of a project. This unit can be simple or composite, i.e. contain other Blocks.

_Element_ - part of the Block, responsible for a particular function. It may be only a part of the Block and does not make sense in isolation from Block.

_Modifier_ - property of a Block or Element that changes the appearance or behavior. Has a name and a value. Simultaneously can be used several different modifiers for one Block or Element.

### Syntax
##### Block
If the name of the Block consists of several words, then they are separated by a hyphen

```
.menu, .product-categories
```

##### Element
Element element consists of the name block, double underscore and the name of the element. For a composite element name you want to use a hyphen.

```
.menu__item, .menu__promo-link
```

##### Modifier 
Modifier selector consists of a block (or element) name, a double hyphen, name modifier, underscore, and the modifier value.

```
.menu--theme_categories, .menu__item--type_promo
```

### Important features

* BEM-methodology excludes the using of id-type selectors to describe the styles (to avoid the high specificity and providing the possibility of re-using a Block). Only class-type selectors allowed for style declaration.
* Selector name should not be too abstract and at the same time should not describe the content (for example, instead of '.red' you can use '.title-error').
* Selector must not include html-tags because we want to get context-independent units.
* Name of the class should be as short as possible, but at the same time is so long to save the sense.
* The names of Blocks, Elements and Modifiers should reflect as clearly as possible the meaning of the described unit.
* Cascading selectors should be excluded from CSS. Cascade is possible only in one case: .[modifier] .[element]

More information about BEM you can read on <http://bem.info>


# Order of the selector's properties

To increase the productivity of working with code, it is important save the same order of describing the properties. All style properties are divided into 4 types: Position, Display & Box model, Typography and Other decoration styles.

Example:

```
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

# Separation of CSS-files

Each Block is described by a separate CSS-file and there is only one CSS-file which describes one Block. CSS-file for Block also includes Elements and Modifiers of the Block. Name of the CSS-file is equivalent to the Block name (for example, menu.css, product.css).

Global styles should be presented in separated CSS-file (basic.css).


# Comments 

CSS-files for a Block must begin with the title comment.

```
/*------------------------------------*\
    
    #BLOCK-NAME

    About this block, about elements and modifiers for this block.

    HTML sample:
    <div class="menu menu--type-main">
    	<div class="menu__logo">
    	</div>
    </div>

\*------------------------------------*/
```

Comment for selector:

```
/**
 * Some comment
 */
```

TODO-comment for selector:

```
/**
 * TODO: some comment
 */
```

Each of selector's properties can have own explanatory comments:

```
.btn--type_order {
    background-color: #ddd; /* TODO: drop color value to variable */
    text-decoration: none !important; /* preventing default .a behavior */
}
```

# Line breaks

Line breaks in CSS-files used for the visual distinction. 

1 line break - to close within the meaning of selectors (elements of one block, one block modifiers) 

2 line break - different in the sense of the selectors (element and modifier of one block)

```
/*------------------------------------*\
    
    #SECTION-TITLE

    Description (about this block, about elements and modifiers for this block)

    Sample HTML-template

    <div class="menu menu--type-main">
    	<div class="menu__logo">
    	</div>
    </div>

\*------------------------------------*/

.product__picture {
	
}

.product__title {
	
}


/*
    ##PRODUCT--TYPE
 **************************************/

.product--type_product-page {
	
}

.product--type_grid {
	
}
```

# Z-index

Z-index value depends on the context of use:

1. Page elements: 1-300.
2. Popup elements on page: 101 - 300.
3. Modal windows: 301-600.
4. Popup elements in modal windows: 601-900.


##SASS

Limit nesting level by one and exclude cases with nesting level of 2 or more.
For nested BEM-selector to apply & 
Nested selectors should be indented from the left. 
Nested selectors must be separated by one blank line above and below.

```
***WRONG***

.ecard {  
.ecard__header {
.ecard__header--theme_confirmation & {
	font-weight: bold;
}
}
}

***RIGHT***

.ecard {  
					/* 1 пустая строка перед вложенным селектором */
	&__header {		/* & помогает устранить повторение название блока в 				названии элемента */
		
	}
				    /* 1 пустая строка после вложенного селектора */
}

.ecard--theme_confirmation {
					/* вложенные декларации имеют отступ слева */
	.ecard__title {
		font-weight: bold;
	}

}
```

Все переменные должны находиться в отдельном файле vars.scss
Для удобства поддержки CSS в переменных должны быть определены все значения для свойств font-size, font-family, line-height, color, background-color, z-index, min-width and max-width для @media

```
$font-size-s: 1.2em;
$font-size-m: 1.4em;
$font-size-l: 1.6em;

$line—height-s: 1.4;
$line—height-m: 1.6;
$line—height-l: 1.8;

$font-family-sans: Arial, Tahoma, Verdana, sans; 
$font-family-serif: ’Times New Roman’, Times, Georgia, sans-serif;

$color-text: #333;
$color-note: #999;
$color-link: #000;
$color-link-hover: #ff0000;

z-page:

min-width-mobile:
max-width-mobile:

min-width-tablet:
max-width-tablet:

min-width-screen:
max-width-screen:

min-width-widescreen:
max-width-widescreen:

Все глобальные и базовые стили должны находиться в файле basic.scss



// Media queries
// ---------------------------------------------------------------------
@mixin breakpoint($point) {
    @if $point == l {
        @media (max-width: 1600px) { @content; }
    }
    @else if $point == m {
        @media (max-width: 1250px) { @content; }
    }
    @else if $point == s {
        @media (max-width: 650px)  { @content; }
    }
}
 
// .module {
//   width: 25%;
//   @include breakpoint(s) {
//     width: 100%;
//   }
// }
```


## HTML tags

Верстка по стандарту HTML5
<!DOCTYPE html>

Порядок следования атрибутов в html-тэге:

```
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

```
<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}
```

TODO комментарий:

<!-- TODO: remove optional tags -->

Верстка должна быть семантической, выбор тэга должен быть обусловлен его предназначением:

```
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>
<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

Все картинки должны иметь аттрибут alt

```
<!-- Not recommended -->
<img src="spreadsheet.png">
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

В тэгах <link> и <script> для ссылки на CSS и Javascript соответственно нет необходимости в аттрибуте type, его можно опустить

```
<!-- Not recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css" type="text/css">
<!-- Recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">
```

```
<!-- Not recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js" type="text/javascript"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

HTML5 позволяет
Для ясности кода мы используем закрывающие тэги в стиле XML:

```
<ul>
<li></li>
<li></li>
</ul>
```

А для одиночных тэгов нет необходимости использовать /:

```
<br>
<img src=“”>
```

## id attribute

At the same time, the html-tag may have the attribute 'id', which will work for javascript. Classes and id, are intended to work only with javascript should not receive any decoration styles and always should be prefixed with 'js-'.


## Responsive design

* Font size can be specified in '%', 'em' or 'rem' (with callbacks in 'em' for old browsers). You can not specify the font size in fixed units like 'px' or 'pt'. *Exception:* 'pt' can only be used for the printed version of the page. 
* Do not specify a unit of measurement for the 'line-height'. So 'line-height' will be designed proportionally to the current font size.

```
line-height: 1.4;
```

* Do not use <table> for layout
* For padding it is desirable to use em instead of px
* All responsive pages should have 'viewport' meta-tag
 
```
<meta name="viewport" content="width=device-width, initial-scale=1">
```

* Following to Mobile-first style we should use only 'min-width' for media queries

```
@media all and (min-width: 50em) {...}
```