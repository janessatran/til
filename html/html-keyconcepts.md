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
