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
p {
  color: orange;
  font-size: 16px;
}
```

#### Common Selectors Overview
| Example | Classification | Explanation |
|---------|----------------|-------------|
| h1      | Type Selector  | Selects an element by its type |
| .tagline | Class Selector | Selects an element by the class attribute value, which may be reused multiple times per page. |
| #intro | ID Selector | Selects an element by the ID attribute value, which is unique and to only be used once per page. |

CSS
```CSS
h1 {...}
.tagline {...}
#intro {...}
```

HTML
```HTML
<section id="intro">
    <h1>....</h1>
    <h2 class="tagline">....</h2>
</section>
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

#How can you shorten up a long batch of CSS that’s doing the same thing to many different elements by putting them all in one line?

#How do you target the immediate child of an element?
By using `>` between the parent and child element.
CSS
```CSS
article > p { ... }
```

HTML
```HTML
<p>...</p>
<article>
  <p>This paragraph will be selected</p>
  <div>
    <p>...</p>
  </div>
</article>
```

#### Child Selectors Overview
| Example | Classification | Explanation |
|---------|----------------|-------------|
| article h2      | Descendant Selector  | Selects an element that resides anywhere within an identified ancestor element. |
| article > p | Direct Child Selector | Selects an element that resides immediately inside an identified parent elemebt. |

#How do you target a class inside a class?
```CSS
.parent .child {
    /* styles */
}
```

#How do you target a class inside an ID?
```CSS
#idName .className {
    /* styles */
}
```
#How would you target “all the links inside li elements that have the class bunny which are inside the unordered list with the id things-that-hop”?
```CSS
ul #things-that-hop .bunny li {
    /* styles */
}
```

#What are the three ways to include CSS in your project?
1. External Style Sheet
2. Internal Style Sheet
3. Inline Style

#### External Style Sheet

```HTML
<head>
    <link rel="stylesheet" type="text/css" href="styles.css">
</head>
```
#### Internal Style Sheet
Internal styles are defined within the `<style>` element inside the `<head>` section of an HTML page.
```HTML
<head>
<style>
body {
  background-color: linen;
}

h1 {
  color: maroon;
  margin-left: 40px;
} 
</style>
</head>
```

#### Inline Styles
An inline style can be used to apply a unique style for a single element
```HTML
<h1 style="color:blue;margin-left:30px;">This is a heading! :D</h1>
```

#What is the browser’s default stylesheet?
Every browser has its own default "user agent' stylesheet that it uses to make unstyled websites appear more legible. For example, most browsers by default make links blue and visited links purple, give tables a certain amount of border/padding, etc. 


#What is a “CSS Reset” file and why is it helpful?
A **CSS Reset** enables CSS authors to force every browser to have all its styles reset to null, thus avoiding cross-browser differences as much as possible. 

#Which stylesheet has preference if you import multiple ones and there are overlapping styles?
The last one that is referenced will have precendent. For example:
```HTML
<link rel="old stylesheet" href="path/to/style.css" />
<link rel="newer stylesheet" href="path/to/style.css" />
<link rel="newest stylesheet" href="path/to/style.css" />
```
In the example above, the last stylesheet will be used.

#What is the order of priority of selectors (e.g. if you specify that the <body> has color black but `<h1>` tags have the color blue but class `main-title` has the color red, which will be used by `<body style="color:yellow"><h1 class="main-title" style="color:green">Howdy!</h1><body>?)`
