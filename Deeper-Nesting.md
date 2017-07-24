Out of the box Slate only supports one level of nesting in the table of contents. However it's possible to get a deeper nesting by making small changes. 

* [Adding support for new static ToC](#static-table-of-contents)
* [Adding support for Slate 1.x](#legacy-slate-1x-tocify-javascript-table-of-contents)

## Static Table of Contents

If you are using the static table of content (not tocify), you'll be making changes in `source/layouts/layout.erb`, `source/stylesheets/screen.css.scss`, and `source/javascripts/all_nosearch.js`. 

Once you've installed slate open the following file `source/javascripts/all_nosearch.js` 

In the function, you can add more selectors. So if you want two levels of nesting the section with selectors should look like this: `'.toc-link', '.toc-list-h2, .toc-list-h3'`. 

You'll need to add styling for `.toc-list-h3 in the file `source/stylesheets/screen.css.scss` The styling is located on line 178 at the time of writing. 
```CSS
.toc-list-h3 {
  display: none;
  background-color: $nav-subitem-bg;
}
```

Additionally, you'll also likely want to make another change in this same file to keep code examples on the same level as their appropriate explanations. This change needed would be located on line 377 at the time of writing.
```CSS
// the div is the tocify hidden div for placeholding stuff
& > h1,
& > h2,
& > h3,
& > div {
  clear: both;
}
```

You'll also need to make a small change in `source/layouts/layout.erb`. The change needed would be located on line 80 at the time of writing. 
```ruby
<% if h2[:children].length > 0 %>
  <ul class="toc-list-h3">
    <% h2[:children].each do |h3| %>
      <li>
        <a href="#<%= h3[:id] %>" class="toc-h3 toc-link" data-title="<%= h1[:content] %>"><%= h3[:content] %></a>
      </li>
    <% end %>
  </ul>
<% end %>
```

## Legacy (Slate 1.x) Tocify JavaScript Table of Contents

`Tocify` supports deeper nesting with a couple small changes. Once you've installed slate open the following file `source/javascripts/app/toc.js` 

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
