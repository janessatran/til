# The Box Model
Taking notes while going through: [https://www.theodinproject.com/lessons/the-box-model](https://www.theodinproject.com/lessons/the-box-model)

# Learning Outcomes
- What’s the difference between margin and padding?
- How do borders affect the size of the box?
- How can margins be used to center an element horizontally on the page?
- What does it mean that “margins are collapsed”?
- What is the difference between block, inline-block and inline elements when thinking about the box model?
- When are you required to specify the width of an element vs letting the browser figure it out for you?
- How do box shadows affect element box sizing?
- How can you check an element’s box model in your developer tools (it’s a helpful graphic)?

# Notes
- `block-level` elements occupy any available width, regardless of their content, and begin on a new line. 
  - generally used for larger pieces of content, such as headings and structural elements
- `inline-level` elements occupy only the width their content requires and line up on the same line, one after the other.
  - generally used for smaller pieces of content, such as a few words selected to be bold or italicized
- `inline-block` will allow an element to behave as a block-level element, accepting all box model properties, however, the element will be displayed in line with other elements and not begin on a new line by default
