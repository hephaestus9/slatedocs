Out of the box Slate only supports one level of nesting in the table of contents. However it's possible to get a deeper nesting as the plugin `tocify` supports that. Once you've installed slate open the following file `source/javascripts/app/toc.js` 

In the function makeToc you can add more selectors. So if you want two levels of nesting the section with selectors should look like this: `selectors: 'h1, h2, h3'`. Now you have two levels on nesting! 

But you probably want to style the levels of nesting differently. You can add a different styling in the file `source/stylesheets/screen.css.scss` The styling is located on line 192 at the time of writing. For every level of nesting that you have, you need to add another `.tocify-subheader` to get to the appropriate styling. 

```CSS
.tocify-subheader {
  .tocify-subheader {
    .tocify-item>a {
      // Styling here for a level 2 nesting. For example -> 
      padding-left: $nav-padding + $nav-indent * 2;
      font-size: 12px;
    }
  }
}
```