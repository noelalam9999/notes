#HTML and CSS
##Position
- Defaults to static, which means the element is positioned according to the normal flow of the document.
- Elements can be custom positioned with relative, absolute, fixed, or sticky.
  - relative means relative to its static position.
  - absolute means relative to the first parent with a position other than static (defaults to window).
  - fixed means the element is removed from the normal document flow, and stays in a fixed position relative to the viewport.
  - sticky toggles between relative and fixed, depending on the scroll position. It is positioned relative until a given offset position is met in the viewport where it “sticks” in place (i.e. fixed).

## Display
- The default value depends on the HTML tag used.
- inline means elements flow horizontally.
- block means elements occupy all the horizontal available space.
- inline-block behaves like inline, but you can set width, height, vertical margin and padding.
- flex means that outside behaves like a block, but inside you can use the flexbox model.
- grid means that outside behaves like a block, but inside you can use a two-dimensional grid system.
- none means the element and all of its descendants are excluded from the DOM.

## Flexbox
- Allows to define layout rules that are more declarative, and that adapt as the viewport size changes.
- Is made of a container (parent) and items (children).
- Applies only to direct (first-level) children of the container.
- Properties of a flex container are: flex-flow, flex-wrap, justify-content, align-items, and align-content.

##Box-sizing
- Describes whether the width and height values should be considered inclusive of the padding and border (border-box) or not (content-box, default).

##Z-index
- Is the third dimension in the document space, and describes how elements stack on top of each other.
- Is applied only to custom-positioned elements.
- The numeric value is always relative to the containing stacking context.

## Media queries
- Are used for responsive design.
- Define the breaking points to apply custom CSS rules as the viewport size changes.

##Vendor prefixes
- Are required for declaring newly-introduced CSS rules that are not part of the standard yet, but are supported by some browser vendors.

## Transformations
- Allow to graphically transform elements in the document plane.
- Available transformations include: matrix, perspective, rotate, scale, skew, and translate.

##Animations
- Allow to animate a progressive change in CSS rules.
- Are set-up with a total duration, timing function, direction and iterations count (the last two are optional).
- Specific custom points in the animation are defined through keyframes, indicated as percentage progression of the total animation.

## Pre-processors
- Extend CSS syntax (e.g. nested rules, mixins, etc.)
- Common CSS pre-processors are LESS, SASS, cssnext.
- The file with the custom rules needs to be transpiled to regular CSS before it can be interpreted by the browser.

##Frameworks
- Are libraries that provide pre-built CSS rules for common use cases.
- Common CSS frameworks are Bootstrap, Materialize, Bulma, and Tailwind.
- Allow to quickly prototype a functional UI, but can be cumbersome if you later decide to customize styles.