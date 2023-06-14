---
title: css flex to reverse list
date: 2023-06-14T18:08:35.840Z
tags:
  - css
  - webdev
---
it's not wise to reverse list using javascript `.reverse()` to render `v-for`. Because i encountered crashing apps, the best way is to use flexbox reverse like this:
```css
ul {
  display: flex;
  flex-direction: column-reverse;
}
```