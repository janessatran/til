# Fundamentals of CSS 
Questions from The [The Odin Project](https://www.theodinproject.com/courses/html5-and-css3/lessons/css3-basics)

## Questions/Topics Covered:
- [How do you declare a variable?](#How-do-you-declare-a-variable?)

## Questions and Answers:

<h3 id="selectors">
    What are selectors?
</h3>

**Selectors** designate which elements within our HTML we want to target/style. They can be as general or as specific as we want, for example, we could select every paragraph on a page or we might select only one specific paragraph on a page. 
- Selectors generally target an attribute value, such as an `id` or `class` value.
- Sometimes they target the type of element, such as `<h1>` or `<p>`.

Example of targeting all the `<p>` elements in your document:
```CSS
p { ... }
```

### In general, how specific should you be when targeting elements using selectors?
In general, you want to try to structure your code to use classes rather than IDs, and you want to use classes in selectors to apply styles (instead of IDs). IDs should not be used as selectors (generally) because these rules are too tightly coupled with the HTML, with no possibility of reuse (and we want to be able to re-use our code...).

What’s the difference between using %, em and rem to specify sizes?
- `em` is relative to the parent's font size; it gives us the ability to control an area of a design.
- `rem` is relative to a base font-size (root em); it gives us the ability to scale type across the entire page easily.

By setting all units to `rem`, we have the following advantages:
- We can scale our whole application with one CSS media query where we specify the font size. By altering the font size, all the elements which have `rem` will scale accordingly.
- When users aren't using the default browser font size, our application will scale with the selected font size of the user.

How do you select an element inside another element?
Use the descendant selector (a space) between the parent element and the descendant element.
Example:
```CSS
div.main p.intro {
   /* CSS rules */
}
```
In the case above, the rules applied to the `p` of class `intro` will only apply if its ancestor is a `div` of class `main`. 

#How can you shorten up a long batch of CSS that’s doing the same thing to many different #elements by putting them all in one line?

#How do you target the immediate child of an element?

#How do you target a class inside a class?

#How do you target a class inside an ID?

#How would you target “all the links inside li elements that have the class bunny which are #inside the unordered list with the id things-that-hop”?

#What are the three ways to include CSS in your project?

#How do you import an external stylesheet?

#What is the browser’s default stylesheet?

#What is a “CSS Reset” file and why is it helpful?

#Which stylesheet has preference if you import multiple ones and there are overlapping styles?

#What is the order of priority of selectors (e.g. if you specify that the <body> has color black but `<h1>` tags have the color blue but class `main-title` has the color red, which will be used by `<body style="color:yellow"><h1 class="main-title" style="color:green">Howdy!</h1><body>?)`