## Responsive CSS

[Codepen](https://codepen.io/tim-corley/pen/wvGMpvW)

/home/tim/GitHub/iamshaunjp/psd-to-wp

### media queries

```css
@media (min-width: 600px) {
  /*MOBILE FIRST*/
}

@media (max-width: 900px) {
  /*DESKTOP FIRST*/
}
```

when the viewport is at 900px or below, show a different style:
`@media (max-width: 900px) {...}`

when the viewport is at 600px or above, show a differnet style:
`@media (min-width: 600px) {...}`

stylesheet starter template:

```
/* VARIABLES */
/* RESET */
/* BASE STYLES */
/* FONTS */
/* MOBILE STYLES */
/* SMALL TABLET STYLES */
@media (min-width: 620px) {
}

/* LARGER TABLET / LAPTOPS STYLES */
@media (min-width: 960px) {
}

/* DESKTOP STYLES */
@media (min-width: 1200px) {
}
```
