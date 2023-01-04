# Development-Guide-Lines

**HTML**

All markup must be [context driven and semantic](https://developer.mozilla.org/en-US/docs/Glossary/semantics) and should make extensive use of HTML5 tags. Hierarchical and semantic markup of content allow it to be properly interpreted by a browser on any device, assistive technology, or as an HTML document devoid of styling.

Closing tags must be added and elements must be nested according to the [W3C specification](https://html.spec.whatwg.org/). Elements must not contain duplicate attributes and IDs must be unique.

Tag and attribute names must always be lowercase.

**Good:**

```
<body>
  <header class="site-header">
    <nav>...</nav>
  </header>

  <main>
    <article>
      <header>
        <h1>...</h1>
      </header>

      <section>...</section>
      <footer>...</footer>
    </article>
  </main>

  <footer class="site-footer">...</footer>
</body>
```

Bad:

```
<body>
  <div class="site-header">
    <div class="navigation"> ... </div>
  </div>

  <div class="main">
    <div class="article">
      <div class='header'>
        <h1> ... </h1>
      </div>
      
      <div class='section'> ... </div>
      <div class='footer'> ... </div>
    </div> 
  </div>
	
  <div class="site-footer"> ... </div>
</body>
```

Over reliance on <div> or <span> tags indicate that more semantic markup can be used.

**Resources**

- [Semantic HTML on Codecademy](https://www.codecademy.com/learn/learn-html/modules/learn-semantic-html)

- [Semantics on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)

- [HTML elements reference on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

- [HTML attributes reference on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)

Content should follow a clear and sensical hierarchical flow.

**Good:**
  
```
<article>
  <h1>Semantics in HTML</h1>

  <img src="/path/to/image.jpg" alt="text describing the image">
 
  <section>
    <h1>Section title</h1>
    <p>!-- ... --><p>
    
    <h2>Sub-Section title</h2>
    <p><!-- ... --></p>
  </section>
  
  <footer>
    <h2>Related Links</h2>
    
    <ul>
      <li>
        <a href="path/to/resource">Resource</a>
      </li>
       <li>
        <a href="path/to/another-resource">Another Resource</a>
      </li>     
    </ul>
  </footer>
</article>
```  
  
**Bad:**

```
<article>
  <img src="/path/to/image.jpg" alt="text describing the image">
  <h1>Semantics in HTML</h1>
 
  <section>
    <h3>Section title</h3>
    <p>!-- ... --><p>
    
    <h1>Sub-Section title</h1>
    <p><!-- ... --></p>
  </section>
  
  <footer>
    <h4>Related Links</h4>
    <p><a href="path/to/resource">Resource</a></p>
    <p><a href="path/to/another-resource">Another Resource</a></p>
  </footer>
</article>
```
  
**Attributes**
Use double quotes for attribute values.

**Good:**

```
<a href="https://www.mooveguru.com" class="button" target="blank">Button</a>
```
  
**Bad:**

```
<a href='https://www.mooveguru.com' class="button" target='blank'>Button</a>
```
  
**Accessibility**
	
Using semantic markup is a great start to accessibility as assistive technologies understand semantics and the hierarchy of an HTML document. That said, sometimes additional context is needed. In those instances, the accessibility tree can be extended and adjusted using the following methods.

**WAI-ARIA**
	
The appropriate [ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA) attributes as well as `title`, `alt`, and `role` attributes may be used to extend the accessibility tree and to provide context for content when the context is not evident by the content itself. 

Take great care with ARIA attributes, however, as poor implementation of these attributes can result in a page that is less usable than if no ARIA attributes were used at all. Effort must be made to fully understand them before using them.

Resources

-[Introduction to Aria on Google Web Fundamentals](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/)

- [ARIA on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)

- [WAI-ARIA Overview on w3c.org](https://www.w3.org/WAI/standards-guidelines/aria/)

- [Introduction to ARIA - Accessible Rich Internet Applications on WebAIM](https://webaim.org/techniques/aria/)

**Language**
	
The language of the page (or in some instances, elements through the page) must be identified using the lang attribute.

`lang` reference on [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/lang)

**Tabindex**
	
A logical tab order is typically created by the browser by default through semantic markup and in most instances this is preferable as explicitly setting tabindex values may introduce unintended bugs.

In some instances it may be necessary to specify a tab order which follows relationships in the content without following the reading order of the elements in the code as the default tab order only includes interactive elements. If it is necessary to include non-interactive elements in the tab order, the tab order can be set explicitly for any element. tabindex can also be used as a means to allow focus to be set to components such as dialogs and menus, whose location in the DOM is not adjacent to their respective trigger controls. In such cases, focus can be sent via scripting to the relevant component, where that component's container element, or one of its child elements, has a tabindex value. This will allow the logical tab order to be maintained, while also dynamically correcting the reading order of the page.

`tabindex` on [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex).

**Skip to Content**
	
[“Skip to Content”](https://css-tricks.com/how-to-create-a-skip-to-content-link/) links must be provided.

**Assets**
	
Included assets must be optimized to improve page load speeds. Where appropriate, use rel="preload" and rel="preconnect". <script> tags must include async and defer tags except in instances where asynchronous or deferred loading will provide a prohibitive experience for users.

**References**

- [Link types: preload on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload)

- [Link types: preconnect on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preconnect)

- [Using rel=”preconnect” to establish network connections early and increase performance by Chris Coyier](https://css-tricks.com/using-relpreconnect-to-establish-network-connections-early-and-increase-performance/)

- [Preload, Prefetch And Priorities in Chrome by Addy Osmani](https://medium.com/reloading/preload-prefetch-and-priorities-in-chrome-776165961bbf)

- [Resource Hints - What is Preload, Prefetch, and Preconnect? by Brian Jackson](https://www.keycdn.com/blog/resource-hints)

- [The Script Tag: Attributes on Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script#attributes)

**Tags**
	
**Forms
Inputs**
Form inputs must use the appropriate type for the desired user input.
**
Good**: ```<input type="tel" name="phone">```
**
Bad**: ```<input type="text" name="phone">```

Where appropriate, proper input purposed should be provided.
```
<label for="contact-first-name">First Name</label>
<input type="text" id="contact-first-name" name="first-name" autocomplete="given-name">

<label for="contact-last-name">Last Name</label>
<input type="text" id="contact-last-name" name="last-name" autocomplete="family-name">bels
 ```
	
**Labels**
	
All form inputs must have labels that are linked using the for attribute. Labels must be descriptive and distinct (or otherwise distinguishable). Required fields or fields that require a specific format, value, or length must provide this information within the label.

**Good:**

```
<label for="contact-email">Email Address</label>
<input type="email" id="contact-email">
```	
	
**Bad:**
	
```
<label>Email Address</label>
<input type="email">	
```
	
`for` attribute on [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/for)

**Head**
	
The `<head>` tag should always include the [viewport meta tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Viewport_meta_tag):

```<meta name="viewport" content="width=device-width, initial-scale=1">```
	
**Headers**
`<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, `<h6>` should be context driven, not style driven and must follow the proper hierarchy.

**Images**
Images must always contain the appropriate alt attribute unless they are purely decorative.


```<img src="path/to/image.png" alt="{DESCRIPTIVE TEXT}">```
	
In the case of decorative images, such as icons, the aria-hidden attribute may be used to hide it from assistive technologies.


```<img src="path/to/icon.svg" aria-hidden="true">```
	
**Formats**
	
SVGs should be used wherever possible, such as for icons and illustrations. JPGs are preferred to PNGs if transparencies are not necessary. Images must be sized properly (i.e. resized, not scalled, to fit their container) and must be stripped of meta data and otherwise optimized for the web.

Do not use icon fonts.

**Tables**
	
Complete table markup must always be provided.

Good:

```
<table>
  <caption><!-- ... --></caption>
    <thead>
      <tr>
        <th><!-- ... --></th>
      </tr>
    </thead>

    <tbody>
      <tr>
        <td><!-- ... --></td>
      </tr>
    </tbody>
	
    <tfoot>
      <tr>
        <td><!-- ... --></td>
      </tr>
    </tfoot>
</table>
```
  
**Bad:**

```
<table>
  <caption> ... </caption>
  <tr>
    <th> ... </th>
  </tr>

  <tr>
    <td> ... </td>
  </tr>
  
  <tr>
    <td> ... </td>
  </tr>
</table>
```
 
