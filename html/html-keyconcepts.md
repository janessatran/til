# HTML Key Concepts
### My notes from Codeacademy's learn HTML course

*Document type declaration:*
- the document type declaration `<!DOCTYPE html> is required as the first line of an HTML document
- doctype declaration is an instruction to the browser about what type of document to expect and which version of HTML is being used

*HTML element:*
- the `<html>` element, the root of an HTML document, should be added after the doctype declaration 
- all content/structure for an HTML document should be contained between the opening and closing `<html>` tags

*The head element:*
- the `<head>` element conatins general info about an HTML page that isn't displayed on the page itself
- this information is called metadata and includes things like the title of the HTML document and links to stylesheets

*Title element:*
- the `<title>` element conatins a text that defines the title of an HTML document
- the title is displayed in the browser's title bar or tab in which the HTML page is displayed
- the `<title>` element can only be contained inside a document's `<head>` element

*Anchor element:*
- the anchor element, `<a>`, is used to create hyperlinks in an HTML document
- the hyperlinks can point to:
  - other webpages
  - files on the same server
  - location on the same page
  - any other URL
- `<href>` stands for hyperlink reference attribute; determines the location the anchor element points to

*Target attribute:*
- the `target` attribute on an anchor `<a>` element specifies where a hyperlink should be opened
- for exaxmple, a `target` value of `"_blank"` will tell the browser to open the hyperlink in a new tab in modern browsers, or in a new window in older browsers, or if the browser has had settings changed to open hyperlinks in a new window
  
*File paths:*
- URL paths in HTML can be absolute paths or a relative path
- absolute: full path
- relative: links to a local file in the same folder or on the same server
  - relative paths begin with `./` followed by a path to a local file
  - `./` tells your browser to look for the file path from the current folder
  
*HTML anchor tags:*
- HTML anchor `<a>` tags can surround hyperlink content to a specified url
- they can be applied to many different kinds of content, including `<img>` elements

*Linking to location in same document:*
- the HTML anchor element `<a>` can create hyperlinks to different parts of the same HTML document using the href attribute to point to the desired location with `#` followed by the id of the element to link to. 
```html
<div> 
  <p id="id-of-element-to-link-to">Jump to a different part of the page!</p>
</div>
<a href = "#id-of-element-to-link-to">Take me to a different part of the page</a>
```
*Whitespace in HTML:*
- whitespace added to an HTML document between block level elements will generally be ignored by the browser
- whitespace is added for organization and easier reading of the document itself

```html
<p>Test paragraph</p>

<!-- The whitespace created by this line, and above/below, is ignored by the browser-->

<p>Another test paragraph, which will sit right below the first one</p>
```
*Identing nested HTML code:*
- html code should be formatted such that the indentation of text increases once for each level of nesting
- the 13c standards recommend two spaces of indentation per level of nesting

*Comments in HTML:*
- add comment between `<!--` and `-->`

*HTML alt attribute:*
- an `<img>` element can have alternative text via the `alt` attribute 
- the alternative text will be displayed if an image fails to render due to an incorrect URL, if the image format is not suported by the browser, if the image is blocked from being dispalyed, or if the image has not been recieved from the URL
- the `alt` text will also be read aloud if screen reading software is used to help support visually impaired individuals

```html
<!DOCTYPE html>
<html>
  <head>
    <!-- metadata is contained in this element-->
    <title> Title of HTML Page</title>
    <a href=”https://developer.mozilla.org/en-US/docs/Web”>The URL for this anchor element is an absolute file path.</a>
    <a href=”./about.html”>The URL for this anchor element is a relative file path.</a>  </head>
<html>

```
