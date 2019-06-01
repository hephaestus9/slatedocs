In the `source/stylesheets/screen.css.scss` file, import your fonts after the `general stuff` comment:

```CSS
@import url("https://fonts.googleapis.com/css?family=Roboto");html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%
}
```

Then, change the `%default-font` part in the `source/stylesheets/_variables.scss` file to include your font first:

```CSS
%default-font {
  font-family: Roboto, -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
  font-size: 14px;
}
```