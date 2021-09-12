# Development-Guide-Lines

In general, CSS should be written in such a manner that components are build on top of each other, rather than overriding one another.

Relative units, such as em and rem should be favored over fixed units such as px. Font sizing must never use px.

Properties must be arranged in alphabetical order.
**
**Naming****
As with variables, always use singular naming for readability. Use kebab-case.

**Good:**

```
<ul class="contact-list">
  <li class="contact"><!-- ... --></li>
  <li class="contact"><!-- ... --></li>
</ul>
```

**Bad:
**
```
<ul class="contacts">
  <li class="contact"><!-- ... --></li>
  <li class="contact"><!-- ... --></li>
</ul>
```

Abbreviations are to be avoided except in cases where it does not obstruct the ability for a maintainer to easily and unquestionably understand the component it is describing.

Good: 

```
.txt-center{
  //...
}
```

Acceptable:

```
.bg-img{
  // ...
}
```

Bad:

```
.ctn{
  // ...
}

.pd20{
  // ...
}
```

**Utility Classes**
Utility class names must be descriptive of what they do. They should follow a property-value naming contention:

**Good:**

```
.float-right {
  float: right;
}

.bg-contain {
  background: contain;
}

.text-center {
  text-align: center;
}
```

**Bad:**

```
.right {
  float: right;
}

.contain {
  background-size: contain;
}

.center {
  text-align: center;
}
```
**
Components**
Component class names must describe what they are.
**
Good:**

```
.title {
  // ...
}

.description {
  // ...
}

.post-headline {
  // ...
}
```

**Bad:**

```
.container {
  // ...
}

.wrapper {
  // ...
}
```

Containing or wrapping classes should use the post-fix -area. Classes that drive layout positioning styles may use the post-fix -layout.

```
.blog-title-area {
  // ...
}

.page-layout {
  // ...
}
```

**DOM Structure**
All styling must be done via classes. Tags and IDs are not to be styled. This allows for styles to be easily reusable.

**Good:**
```
.post-list {
  // ...
}
```
**Bad:**
```
ul {
  //...
}
```
**Bad:**
```
#post-list {
  //...
}
```

This allows tags to be interchangeable, since styling is done by class.

```
<!-- These will all have exactly the same styling -->
```
```
<div class="blog-post"><!-- ... --></div>
<article class="blog-post"><!-- ... --></article>
<section class="blog-post"><!-- ... --></section>
```
**Media Queries**
CSS should always follow a mobile-first approach. As such, media queries must favor min-width over max-width where ever possible.

**Good:**
```
@media screen and (min-width: 64em) {
  // ...
}
```
**Bad: **

```
@media screen and (max-width: 64em) {
  // ...
}
```
Media queries must always use em.

**JavaScript Hooks**
Special classes must be used to target elements via JavaScript. These classes must use the prefix js-. Data attributes must be used only for data or configuration storage. Neither must have any effect on styling.

```
<div class="js-map-canvas" data-map-icon="url.png" data-map-lat="4.56"
data-map-lon="1.23"></div>
```

```
const mapList = document.getElementsByClassName('js-map-canvas');

Array.from(mapList).forEach((map: HTMLElement): void => {
  // Initialize map
});
```


