## Basics

[Code Sandbox](https://codesandbox.io/s/css-basics-dm2i1)

[Lynda Course](https://www.lynda.com/CSS-tutorials/Introduction-CSS/578096-2.html?org=bpl.org)

[W3 Specs](https://www.w3.org/Style/CSS/Overview.en.html)

### Cascading Style Sheets

- stylesheet language
- apply css to html either inline or via an external style sheet
- rules are applied from least specific to most specific

### syntax

made up of a **selector** and a **declaration**

```css
p {
  font-family: Arial;
  font-size: 14px;
}
```

- declarations made up of **properties** and **values**

grouping

```css
p,
h1 {
  color: green;
}
```

## selectors

- element
- class
- id
- descendant

combinations

```css
h1.page-title {
  font-size: 28px;
}
```

descendant

```css
div p a {
  color: blue;
}
```

- References:
  - https://htmldog.com/references/css/
  - https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
  - https://tympanus.net/codrops/css_reference/
  - https://www.w3schools.com/css/default.asp
  - https://caniuse.com/
