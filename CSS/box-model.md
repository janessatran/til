# The Box Model
Taking notes while going through: [https://www.theodinproject.com/lessons/the-box-model](https://www.theodinproject.com/lessons/the-box-model)

# Learning Outcomes
#### What’s the difference between margin and padding?
Margin is the outer space of an element, while padding is the inner space of an element.

#### How do borders affect the size of the box?
Borders fall between margin and padding, providing an outline around an element. Adding a border will increase the total width of the element. 

#### How can margins be used to center an element horizontally on the page?
`margin: 0 auto`
- 0 is for top-bottom
- auto is for left-right, which will make it so the margin takes the width of the element and the width of the container.

#### What does it mean that “margins are collapsed”?
When the vertical margins of two elements are touching, the larger margin value will be honored while the smaller one will be collapsed to zero.

#### What is the difference between block, inline-block and inline elements when thinking about the box model?
**Display**:
- `block-level` elements occupy any available width, regardless of their content, and begin on a new line. 
  - generally used for larger pieces of content, such as headings and structural elements
  - default `width` and `height` are 100%
- `inline-level` elements occupy only the width their content requires and line up on the same line, one after the other.
  - generally used for smaller pieces of content, such as a few words selected to be bold or italicized
  - do not have `width` or `height` properties
  - do not have vertical margins, `margin-top` and `margin-bottom` properties
  - padding works on all four sides of `inline` elements, but the `top` and `bottom` padding may bleed into lines above/below an element
- `inline-block` will allow an element to behave as a block-level element, accepting all box model properties, however, the element will be displayed in line with other elements and not begin on a new line by default
- `none` will completely hide an element and render the page as if it doesn't exist

#### When are you required to specify the width of an element vs letting the browser figure it out for you?

#### How do box shadows affect element box sizing?
THey don't. The shadow isn't considered in the final width measuring of the element. 


# Notes

## What is the box model?
The concept that ever element on a page is a rectangular box and may have width, height, padding, borders, and margins.

The total width of an element can be calculated with the formula: 
```
margin-right + border-right + padding-right + width + padding-left + border-left + margin-left
```

The total height of an element can be caluclated with the formula:

```
margin-top + border-top + padding-top + height + padding-bottom + border-bottom + margin-bottom

```

You can set multiple properties for `margin` at once with

```
div {
  margin: 10px 20px; // top bottom left right
}
```

## Borders
Provide an outline around an element. Requires three values: `width`, `style`, and `color`.

```
div {
  border: 6px solid black;
}
```

## Box Sizing
The box model can be changed to support different calculations beyond the additive design, using the `box-sizing` property. This allows us to change exactly how the box model works and how an element's size is calculated. The property accepts three primarily values: `content-box`, `padding-box`, and `border-box`.

Generally speaking, the best `box-sizing` value to pick is `border-box` because it makes the math a lot easier. The main downside of using this property is that it's not supported by every browser. 

### Content Box
This is the default value, leaving the box model as an additive design. 
- The size of an element begins with the width and height properties, and then any padding or margin property values are added from there.

```
 div {
   -webkit-box-sizing: content-box;
   -moz-box-sizing: content-box;
    box-sizing: content-box;
 }
 ```
The hyphens before the `box-sizing` property specify the vendor prefixes. The most common vendor prefixes are:
- Mozilla Firefox, `-moz-`
- Microsoft Internet Explorer: `-ms-`
- Webkit (Google Chrome and Apple Safari): `-webkit-`

### Padding Box
The `padding-box` value alters the box model by including any `padding` property values within the `width` and `height` of an element. For example, when using the `padding-box` value, if an element has `width: 400px` and `padding: 20px`, the actual width will remain 400 pixels. As the `padding` increases, the content size within the element shrinks proportionately. 

However, if we add a `border` or `margin` to it, these values *will* be added to the full box size. So an element with `width: 400px` and `border: 10px` would have a full width of 420 pixels (+10 pixels each side).  

```
div {
  box-sizing: padding-box;
}
```
**Note: padding-box is deprecated and shouldn't be used anymore**

### Border Box
The `border-box` value alters the box model so that any `border` or `padding` property values are included within the `width` and `height` of an element. For example, when using the `border-box` value, the following element has a total width of 400 pixels:

```
#my-element {
  box-sizing: border-box;
  width: 400px;
  padding: 10px;
  border: 10px;
}
```


