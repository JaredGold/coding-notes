# HTML

## Tags

Make sure to close most tags. </>

### Head and Doctype

* First open all html documents with `<!DOCTYPE html>`. This tells the browser the file is of type HTML 5.
* Then `<html> </html>` to tell the browser to interpret everything between this as html code.
* Then `<head></head>` shows what is the meta data of the document.
* `<title></title>` Shows the title seen on the tab.
* To create a comment at any point `<!-- the left starts the comment and the right ends -->`

### Body

#### Basic Importance

* `<body>` Everything after this is going to be visual code to the website
* `<p>` Is a paragraph tag
* `<h1>` is a heading tag. This tag can be any variation from 1-6. 1 being the largest.
* `<div>` is a divider. This is used to split up sections used later in CSS.
* The `<em>` tag will generally render as *italic* emphasis.
* The `<strong>` will generally render as **bold** emphasis.
* `<br>` is a line break. This is used similar to a return when typing in a normal text document. You can use this at any point in the document.
* `<ul>` starts an unordered dot point list. `<ol>` starts an organized list.
* under the list tag we use `<li>` for every list element.
* `<img>` is used to add an image. To use an image tag you must also use a source attribute. `<img src="image.jpg">` is how you would add an image to a site.
* `<video>` is a similar tag to image. Although this tag needs a closing tag. The text in-between the open and close tag will be displayed if the video does not load. This tag also can have a width and height attribute.
* `<a>` Is used for links. Example: `<a href="link.com">This is a link</a>`

#### Table's

* `<table></table>` Creates a table
* `<tr></tr>` Creates table rows
* `<td></td>` Creates Table Data between table rows. Between table data is what you want seen in the tables.
* `<th></th>` Creates Table Headings/titles.
* Note, also, the use of the `scope` attribute, which can take one of two values:
  1. `row` - this value makes it clear that the heading is for a row.
  2. `col` - this value makes it clear that the heading is for a column.
* `colspan="2"` is an attribute that makes that span over multiple different columns. For example this spans over 2 columns.
* `rowspan` is used similarly as above but for rows.
* `<tbody></tbody>` is used similarly to the body element. It should be the parent of the tables  data but not the headings **AND** be the child of the table element.
* `<thead></thead>` is used similar to a heading. This sections it separate to the body.
* `<tfoot></tfoot>` is used to symbolize the bottom of the table.
* Tables visuals should be customized in the CSS

#### Semantic HTML

Semantic HTML is the use of better structured code. For instance not using `div` but using tags that are more appropriate.

* `<header>` is where we put our `<h1-6>` Tags.

* `<nav>` is where you put the navigational bar.

* `<main>` Is where we put the dominant content within the webpage

* `<footer>` contains:

  * Contact information
  * Copyright information
  * Terms of use
  * Site Map
  * Reference to top of page links

* `<section>`  defines elements in a document like, chapters, headings, or any other area of the document with the same theme.

* `<article>` is used to hold articles, blogs, comments, magazines, etc.

* `<aside>` is used for parts of the article that is not required to understand the main content.

  * Bibliographies
  * Endnotes
  * Comments
  * [Pull quotes](https://en.wikipedia.org/wiki/Pull_quote)
  * Editorial sidebars
  * Additional information

* `<figure>` surrounds media (illustration, diagram, code snippet, etc)

* `<figcaption>` is used in the `<figure>` tag to add a caption to describe the image.

* `<audio>` encapsulates sound and audio sources.

  ​		Below is how to create audio.

  ```html
  <audio autoplay controls> <!-- auto plays and has controls -->
    <source src="iAmAnAudioFile.mp3" type="audio/mp3">
  </audio>
  ```

* **(DEPRECIATED)** `<embed>` creates an embedded button to a source of media. **(DEPRECIATED)**

#### Forms + Inputs

[https://www.w3schools.com/html/html_form_input_types.asp](https://www.w3schools.com/html/html_form_input_types.asp )   - Full list of input types and how to use them. More info below in codecademy's short notes

More on regex https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions

* `<form action="/example.html" method="post">` is how a form element looks.

  * The `action` attribute determines where the information is sent.
  * The `method` attribute is assigned a HTTP verb that is included in the HTTP request.

* `<input...>` is how we get the users input inside of the form.

  * we then use `type="text"` or similar types to get what type of input we want.
  * then we use `name="name"` or similar to give the input a name to send with the form. For example if the name is cheese and the response is no it would show as cheese=no.
  * then we use `value="input text here"` or similar to display prefill on it.
  * we can also use `id="name"` to link labels
    * `<input type="text" name="username" value="Input Username">`

* `<label for="name">` goes above the input you wish to attach a label to.

  * the "name" is the name you assigned in the input. 
    * `<label for="username">Username</label>`

* `<select id="id" name="name">` Allows a drop down list

  * To add options we do this as a child of select using: 
    `<option value="pizza">Pizza</option`

* `<datalist...>` is very similar to select but it allows the user to type their response.

* `<textarea>` Allows a response with a larger text area. The size can be modified (check below)

* Putting `required` as an attribute with input will not let you submit the form unless it is filled.

* Putting a `min` and a `max` value forces the `range` and `number` types to fit between that range

* `minlength` and `maxlength` can be used in text fields to limit the amount of characters used.

* You can also use `pattern` to make sure the input follows a specific pattern guide

  * We could use the regex: `[0-9]{14,16}` which checks that the user provided only numbers and that they entered at least 14 digits and at most 16 digits.

  

## Attributes

Attributes are used alongside tags. For example a <div> may also have <div id="shortname">

* `<div id="shortname">` the id tag is used in CSS to manage different sections. This can be used 
* `src="image.jpg"` is added to the img tag to specify which image
* `alt="a brown bear"` alt tags can be used when websites don't load an image it tells the user what meant to be there was whatever the alt was. It also is used in search engine optimization and for vision impaired people to have an audible readout of what the image is.
* `height ="1080" width ="1920"` This can be added to images or videos to force a specific height and width.
* `controls` instructs the browser to show basic video controls. Play and Pause.
* `target="_blank"` opens links in new tabs
* to link to id's on site use `<a href=#idname>`





## Code Cademy Short Notes

#### Basic

- **HTML** stands for **H**yper**T**ext **M**arkup **L**anguage and is used to create the structure and content of a webpage.
- Most HTML elements contain opening and closing tags with raw text or other HTML tags between them.
- HTML elements can be nested inside other elements. The enclosed element is the child of the enclosing parent element.
- Any visible content should be placed within the opening and closing `<body>` tags.
- Headings and sub-headings, `<h1>` to `<h6>` tags, are used to enlarge text.
- `<p>`, `<span>` and `<div>` tags specify text or blocks.
- The `<em>` and `<strong>` tags are used to emphasize text.
- Line breaks are created with the `<br>` tag.
- Ordered lists (`<ol>`) are numbered and unordered lists (`<ul>`) are bulleted.
- Images (`<img>`) and videos (`<video>`) can be added by linking to an existing source.
- The `<!DOCTYPE html>` declaration should always be the first line of code in your HTML files. This lets the browser know what version of HTML to expect.
- The `<html>` element will contain all of your HTML code.
- Information about the web page, like the title, belongs within the `<head>` of the page.
- You can add a title to your web page by using the `<title>` element, inside of the head.
- A webpage’s title appears in a browser’s tab.
- Anchor tags (`<a>`) are used to link to internal pages, external pages or content on the same page.
- You can create sections on a webpage and jump to them using `<a>` tags and adding `id`s to the elements you wish to jump to.
- Whitespace between HTML elements helps make code easier to read while not changing how elements appear in the browser.
- Indentation also helps make code easier to read. It makes parent-child relationships visible.
- Comments are written in HTML using the following syntax: `<!-- comment -->`.

#### Tables

- The `<table>` element creates a table.
- The `<tr>` element adds rows to a table.
- To add data to a row, you can use the `<td>` element.
- Table headings clarify the meaning of data. Headings are added with the `<th>` element.
- Table data can span columns using the `colspan` attribute.
- Table data can span rows using the `rowspan` attribute.
- Tables can be split into three main sections: a head, a body, and a footer.
- A table’s head is created with the `<thead>` element.
- A table’s body is created with the `<tbody>` element.
- A table’s footer is created with the `<tfoot>` element.
- All the CSS properties you learned about in this course can be applied to tables and their data.

#### Forms + Inputs

- The purpose of a `<form>` is to allow users to input information and send it.
- The `<form>`‘s `action` attribute determines where the form’s information goes.
- The `<form>`‘s `method` attribute determines how the information is sent and processed.
- To add fields for users to input information we use the`<input>`element and set the `type` attribute to a field of our choosing:
  - Setting `type` to `"text"` creates a single row field for text input.
  - Setting `type` to `"password"` creates a single row field that censors text input.
  - Setting `type` to `"number"` creates a single row field for number input.
  - Setting `type` to `"range"` creates a slider to select from a range of numbers.
  - Setting `type` to `"checkbox"` creates a single checkbox which can be paired with other checkboxes.
  - Setting `type` to `"radio"` creates a radio button that can be paired with other radio buttons.
  - Setting `type` to `"list"` will pair the `<input>` with a `<datalist>` element if the `id` of both are the same.
  - Setting `type` to `"submit"` creates a submit button.
- A `<select>` element is populated with `<option>` elements and renders a dropdown list selection.
- A `<datalist>` element is populated with `<option>` elements and works with an `<input>` to search through choices.
- A `<textarea>` element is a text input field that has a customizable area.
- When a `<form>` is submitted, the `name` of the fields that accept input and the `value` of those fields are sent as `name=value` pairs.
- Client-side validations happen in the browser before information is sent to a server.
- Adding the `required` attribute to an input related element will validate that the input field has information in it.
- Assigning a value to the `min` attribute of a number input element will validate an acceptable minimum value.
- Assigning a value to the `max` attribute of a number input element will validate an acceptable maximum value.
- Assigning a value to the `minlength` attribute of a text input element will validate an acceptable minimum number of characters.
- Assigning a value to the `maxlength` attribute of a text input element will validate an acceptable maximum number of characters.
- Assigning a regex to `pattern` matches the input to the provided regex.
- If validations on a `<form>` do not pass, the user gets a message explaining why and the `<form>` cannot be submitted.

#### Other

- `<section>` - An element used to represent a standalone section for which a more specific element can’t be found. This usually has a heading as a child element. A section should make sense in the outline of a document, whereas `<div>` is used for styling. This is a semantic element you’ll learn more about in a later lesson.
- `class` - A global attribute that has a list of classes pertaining to an element. You’ll see this used with `<section>` in the practice.
- `<hr>` - An element that is used to a break between paragraph-level elements. It is displayed as a horizontal line. This is also a semantic element that you’ll learn more about in a later lesson.

#### Semantic Code

- Semantic HTML introduces meaning to a page through specific elements that provide context as to what is in between the tags.
- Semantic HTML is a modern standard and makes a website accessible for people who use screen readers to translate the webpage and improves your website’s SEO.
- `<header>`, `<nav>` , `<main>` and `<footer>` create the basic structure of the webpage.
- `<section>` defines elements in a document, such as chapters, headings, or any other area of the document with the same theme.
- `<article>` holds content that makes sense on its own such as articles, blogs, comments, etc.
- `<aside>` contains information that is related to the main content, but not required in order to understand the dominant information.
- `<figure>` encapsulates all types of media.
- `<figcaption>` is used to describe the media in `<figure>`.
- `<video>`, `<embed>`, and `<audio>` elements are used for media files.

