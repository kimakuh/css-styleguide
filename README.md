# MUI CSS Styleguide

The following document outlines a reasonable style guide for CSS development.
These guidelines strongly encourage the use of existing, common, sensible
patterns.

This is a living document and new ideas are always welcome. Please
contribute.


## Table of contents

1. [General principles](#general-principles)
2. [Whitespace](#whitespace)
3. [Comments](#comments)
4. [Format](#format)
5. [Practical example](#example)


<a name="general-principles"></a>
## 1. General principles

> "Part of being a good steward to a successful project is realizing that
> writing code for yourself is a Bad Idea™. If thousands of people are using
> your code, then write your code for maximum clarity, not your personal
> preference of how to get clever within the spec." - Idan Gazit

* Don't try to prematurely optimize your code; keep it readable and
  understandable.
* All code in any code-base should look like a single person typed it, even
  when many people are contributing to it.
* Strictly enforce the agreed-upon style.
* If in doubt when deciding upon a style use existing, common patterns.


<a name="whitespace"></a>
## 2. Whitespace

Only one style should exist across the entire source of your code-base. Always
be consistent in your use of whitespace. Use whitespace to improve
readability.

* _Never_ mix spaces and tabs for indentation.
* Use soft indents (spaces).
* Use 2 spaces per indentation level.
* Use 3 line breaks before an L1 comment block ("===")
* Use 2 line breaks before an L2 comment block ("---")
* Remove trailing end-of-line whitespace



<a name="comments"></a>
## 3. Comments

Well commented code is extremely important. Take time to describe components,
how they work, their limitations, and the way they are constructed. Don't leave
others in the team guessing as to the purpose of uncommon or non-obvious
code.

Comment style should be simple and consistent within a single code base.

* Place comments on a new line above their subject.
* Keep line-length to a maximum 79 columns.
* Make liberal use of comments to break CSS code into discrete sections.
* Use "sentence case" comments and consistent text indentation.

Tip: configure your editor to provide you with shortcuts to output agreed-upon
comment patterns.

Example:

```css
// ============================================================================
// L1-COMMENT-BLOCK
// ============================================================================

// ----------------------------------------------------------------------------
// L2-COMMENT-BLOCK
// ----------------------------------------------------------------------------

/**
 * Short description using Doxygen-style comment format
 *
 * The first sentence of the long description starts here and continues on this
 * line for a while finally concluding here at the end of this paragraph.
 *
 * The long description is ideal for more detailed explanations and
 * documentation. It can include example HTML, URLs, or any other information
 * that is deemed necessary or useful.
 *
 * @tag This is a tag named 'tag'
 *
 * TODO: This is a todo statement that describes an atomic task to be completed
 *   at a later date. It wraps after 80 characters and following lines are
 *   indented by 2 spaces.
 */

// Basic comment that will be removed by the sass compiler

/* This will be left in by the sass compiler */

$myVar: 5px;  // Use inline comments sparingly and with 2 space indent

```


<a name="format"></a>
## 4. Format

The chosen code format must ensure that code is: easy to read; easy to clearly
comment; minimizes the chance of accidentally introducing errors; and results
in useful diffs and blames.

* Use one discrete selector per line in multi-selector rulesets.
* Include a single space before the opening brace of a ruleset.
* Include one declaration per line in a declaration block.
* Use one level of indentation for each declaration.
* Include a single space after the colon of a declaration.
* Use uppercase and shorthand hex values, e.g., `#FFF`.
* Use double quotes consistently.
* Quote attribute values in selectors, e.g., `input[type="checkbox"]`.
* _Where allowed_, avoid specifying units for zero-values, e.g., `margin: 0`.
* Include a space after each comma in comma-separated property or function
  values.
* Include a semi-colon at the end of the last declaration in a declaration
  block.
* Place the closing brace of a ruleset in the same column as the first
  character of the ruleset.
* Separate each ruleset by a blank line.

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  background: #FFF;
  background: linear-gradient(#FFF, rgba(0, 0, 0, 0.8));
  box-sizing: border-box;
  color: #333;
  display: block;
  font-family: "Helvetica Neue", Helvetica, Arial, Sans-Serif;
}

.selector-a,
.selector-b {
  padding: 10px;
}
```

#### Declaration order

Long declaration should be ordered alphabetically within clusters.

```css
.selector {
  // Positioning
  bottom: 0;
  left: 0;
  position: absolute;
  right: 0;
  top: 0;
  z-index: 10;

  // Display & Box Model
  border: 10px solid #333;
  box-sizing: border-box;
  display: inline-block;
  height: 100px;
  margin: 10px;
  overflow: hidden;
  padding: 10px;
  width: 100px;

  // Other
  background: #000;
  color: #FFF;
  font-family: Sans-Serif;
  font-size: 16px;
  text-align: right;
}
```


#### Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line
format. In this case, a space should be included after the opening brace and
before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values - such as collections of gradients or
shadows - can be arranged across multiple lines in an effort to improve
readability and produce more useful diffs. There are various formats that could
be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#FFF, #CCC),
        linear-gradient(#F3C, #4EC);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #CCC inset;
}
```

### SCSS: additional format considerations

The following guidelines are in reference to MUI Sass.

* Limit nesting to 2 level deep. Reassess any nesting more than 2 levels deep.
  This prevents overly-specific CSS selectors.
* Avoid large numbers of nested rules. Break them up when readability starts to
  be affected. Preference to avoid nesting that spreads over more than 20
  lines.
* Always place `@extend` statements on the first lines of a declaration
  block.
* Where possible, group `@include` statements at the top of a declaration
  block, after any `@extend` statements.
* Consider prefixing custom functions with `x-` or another namespace. This
  helps to avoid any potential to confuse your function with a native CSS
  function, or to clash with functions from libraries.
* Consider prefixing custom module-level variables with `x` or another
  namespace. This helps to avoid any potential to confuse your variable with
  other global variables.
* Use camelCase syntax for internal variables.
* Use hyphenated-function-names for SASS functions.
* Use $mui-hyphenated-variable-name for variables that are exposed to
  end users.
* Use mui-hyphenated-function-name for SASS functions that are exposed to
  end users.

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
    height: xCellHeight;
    color: mui-color('red', '500');
    line-height: $mui-base-line-height;
    // other declarations
}
```


<a name="example"></a>
## 5. Practical example

An example of various conventions.

```css
/**
 * Column layout with horizontal scroll.
 *
 * This creates a single row of full-height, non-wrapping columns that can
 * be browsed horizontally within their parent.
 *
 * Example HTML:
 *
 * <div class="grid">
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 * </div>
 */



// ============================================================================
// GRID-LAYOUT
// ============================================================================

/**
 * Grid container
 *
 * Must only contain `.cell` children.
 *
 * 1. Remove inter-cell whitespace
 * 2. Prevent inline-block cells wrapping
 */

.grid {
  font-size: 0; /* 1 */
  height: 100%;
  white-space: nowrap; /* 2 */
}

/**
 * Grid cells
 *
 * No explicit width by default. Extend with `.cell-n` classes.
 *
 * 1. Reset font-size inherited from `.grid`
 * 2. Set the inter-cell spacing
 * 3. Reset white-space inherited from `.grid`
 */

.cell {
  border: 2px solid #333;
  box-sizing: border-box;
  display: inline-block;
  font-size: 16px; /* 1 */
  height: 100%;
  overflow: hidden;
  padding: 0 10px; /* 2 */
  position: relative;
  vertical-align: top;
  white-space: normal; /* 3 */
}

/* Cell states */

.cell.is-animating {
  background-color: #fffdec;
}


// ----------------------------------------------------------------------------
// CELL-DIMENSIONS
// ----------------------------------------------------------------------------

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }


// ----------------------------------------------------------------------------
// CELL-MODIFIERS
// ----------------------------------------------------------------------------

.cell--detail,
.cell--important {
  border-width: 4px;
}
```
