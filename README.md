This is a slightly modified version of Airbnb Css/Sasss Styleguide, or as they call it, "a mostly reasonable approach to CSS and Sass".

Table of Contents
Terminology
Rule Declaration
Selectors
Properties
CSS
Formatting
Comments
OOCSS and BEM
ID Selectors
JavaScript hooks
Border
Sass
Syntax
Ordering
Variables
Mixins
Extend directive
Nested selectors
HTML
Terminology
Rule declaration
A “rule declaration” is the name given to a selector (or a group of selectors) with an accompanying group of properties. Here's an example:

.listing {
  font-size: 18px;
  line-height: 1.2;
}
Selectors
In a rule declaration, “selectors” are the bits that determine which elements in the DOM tree will be styled by the defined properties. Selectors can match HTML elements, as well as an element's class, ID, or any of its attributes. Here are some examples of selectors:

.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
Properties
Finally, properties are what give the selected elements of a rule declaration their style. Properties are key-value pairs, and a rule declaration can contain one or more property declarations. Property declarations look like this:

/* some selector */ {
  background: #f1f1f1;
  color: #333;
}


CSS
Formatting
Use soft tabs (2 spaces) for indentation
Use dashes over camelCasing in class names.
Underscores and are okay if you are using it with BEM syntax.
Do not use ID selectors unless it is the only way you can get an element
When using multiple selectors in a rule declaration, give each selector its own line.
Put a space before the opening brace { in rule declarations
In properties, put a space after, but not before, the : character.
Put closing braces } of rule declarations on a new line
Put blank lines between rule declarations
Bad

.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
Good

.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
Comments
Prefer line comments (// in Sass-land) to block comments.
Prefer comments on their own line. Avoid end-of-line comments.
Write detailed comments for code that isn't self-documenting:
Uses of z-index
Compatibility or browser-specific hacks
OOCSS and BEM
We encourage some combination of OOCSS and BEM for these reasons:

It helps create clear, strict relationships between CSS and HTML
It helps us create reusable, composable components
It allows for less nesting and lower specificity
It helps in building scalable stylesheets
OOCSS, or “Object Oriented CSS”, is an approach for writing CSS that encourages you to think about your stylesheets as a collection of “objects”: reusable, repeatable snippets that can be used independently throughout a website.

Nicole Sullivan's OOCSS wiki
Smashing Magazine's Introduction to OOCSS
BEM, or “Block-Element-Modifier”, is a naming convention for classes in HTML and CSS. It was originally developed by Yandex with large codebases and scalability in mind, and can serve as a solid set of guidelines for implementing OOCSS.

CSS Trick's BEM 101
Harry Roberts' introduction to BEM


Example

// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
.ListingCard is the “block” and represents the higher-level component
.ListingCard__title is an “element” and represents a descendant of .ListingCard that helps compose the block as a whole.
.ListingCard--featured is a “modifier” and represents a different state or variation on the .ListingCard block.
ID selectors
While it is possible to select elements by ID in CSS, it should generally be considered an anti-pattern. ID selectors introduce an unnecessarily high level of specificity to your rule declarations, and they are not reusable.

For more on this subject, read CSS Wizardry's article on dealing with specificity.



Naming Css classes
When naming classes, always use semantic names and not descriptive ones.


Bad

.blue-rectangle {

}



Good

.energy-info-container__energy-used {

}

 
This creates long Css selectors, but helps developers understand the code they are working on. It also creates a really readable Html markup.

JavaScript hooks
Avoid binding to the same class in both your CSS and JavaScript. Conflating the two often leads to, at a minimum, time wasted during refactoring when a developer must cross-reference each class they are changing, and at its worst, developers being afraid to make changes for fear of breaking functionality.

Border
Use 0 instead of none to specify that a style has no border.

Bad

.foo {
  border: none;
}
Good

.foo {
  border: 0;
}
Sass
Syntax
Prefered syntax is indented syntax. 

However, this one is not set in stone. There are pros and cons of both indented and Scss syntax, and neither is better. For that reason, this is subject to change if the FE developers bring good arguments for it to the table. 

Recommended read on that subject is on the Sass lang website:
http://thesassway.com/editorial/sass-vs-scss-which-syntax-is-better

Ordering of property declarations
Property declarations

List all standard property declarations, anything that isn't an @include or a nested selector.

scss .btn-green { background: green; font-weight: bold; // ... }

@include declarations

Grouping @includes either at the beginning makes it easier to read the entire selector.

scss .btn-green { background: green; font-weight: bold; @include transition(background 0.5s ease); // ... }

Nested selectors

Nested selectors, if necessary, go last, and nothing goes after them. Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors. Apply the same guidelines as above to your nested selectors.

scss .btn { background: green; font-weight: bold; @include transition(background 0.5s ease); .icon { margin-right: 10px; } }

Variables
Prefer dash-cased variable names (e.g. $my-variable) over camelCased or snakecased variable names. It is acceptable to prefix variable names that are intended to be used only within the same file with an underscore (e.g. `$my-variable`).

Mixins
Mixins should be used to DRY up your code, add clarity, or abstract complexity--in much the same way as well-named functions. Mixins that accept no arguments can be useful for this, but note that if you are not compressing your payload (e.g. gzip), this may contribute to unnecessary code duplication in the resulting styles.

Think of what Css code you are generating. Scss can produce longer Css files if mixins and nesting are used without this in mind. 
Because of this, when possible, use silent mixins to group classes that share the same rules.

Recommended read on silent mixins:
https://www.thinkful.com/projects/silence-your-css-footprint-with-sass-silent-classes-457/ 

Extend directive
@extend should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using @extend, and you can DRY up your stylesheets nicely with mixins.

Nested selectors
Prefer not using nest selectors more than three levels deep.

.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
When selectors become this long, you're likely writing CSS that is:

Strongly coupled to the HTML (fragile) —OR—
Overly specific (powerful) —OR—
Not reusable
Again: never nest ID selectors!

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should never need to do this.



HTML
Generally, just write valid HTML5, and try avoiding having empty tags, when possible. 



