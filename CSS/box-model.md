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

- you can set multiple properties for `margin` at once with
```
div {
  margin: 10px 20px; // top bottom left right
}
```
