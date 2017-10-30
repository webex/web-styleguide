
### Variables

Prefer kebab cased variable names (e.g. `--my-variable`) over camelCased or snake_cased variable names.

### Global classes

`:global` should be avoided in modules because it can easily cause dangerous behavior that affects other areas of your app.

### Compose directive

Depending on your needs, `compose` is a reasonable way to bring external styles into a module. We have not seen a need for it since CSS Modules can be composed in

```css
.className {
  color: green;
  background: red;
}

.otherClassName {
  composes: className;
  color: yellow;
}
```

### Nested selectors

**Do not nest selectors**


```css
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

Even when using a post processor, we generally avoid using selectors. They encourage overly specific styles that strongly couple styles to HTML structures, and in generally are not reusable.
With any project that already uses a build step, incorporate the CSS Modules pattern into your work instead.



Again: **never nest ID selectors!**

If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should **never** need to do this.

**[⬆ back to top](#table-of-contents)**
