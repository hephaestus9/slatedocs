Out of the box Slate only supports one level of nesting in the table of contents. However it's possible to get a deeper nesting by making small changes. 

* [Adding support for new static ToC](#static-table-of-contents)
* [Adding support for Slate 1.x](#legacy-slate-1x-tocify-javascript-table-of-contents)

## Static Table of Contents

If you are using the static table of content (not tocify), you'll be making changes in 
`source/layouts/layout.erb`, `source/stylesheets/screen.css.scss`, `source/javascripts/all_nosearch.js`, `toc_data.rb` and `source/javascripts/app/_search.js`. 

Documented below is how to add 2 more nesting levels, but you can add as much as you want by deducting from the tutorial how it should be done.

Once you've installed slate open the following file `source/javascripts/all_nosearch.js` 

In the function, you can add more selectors. So if you want three levels of nesting the section with selectors should look like this:

```js
  loadToc($('#toc'), '.toc-link', '.toc-list-h2, .toc-list-h3, .toc-list-h4', 10);
``` 

You'll need to add styling for `.toc-list-h3` (and `.toc-list-h4` etc.) in the file `source/stylesheets/screen.css.scss` The styling is located on line 178 at the time of writing. 
```CSS
.toc-list-h3 {
  display: none;
  background-color: $nav-subitem-bg;
}

.toc-h3 {
  padding-left: $nav-padding + $nav-padding + $nav-indent;
  font-size: 12px;
}

.toc-list-h4 {
  display: none;
  background-color: $nav-subitem-bg;
}

.toc-h4 {
  padding-left: $nav-padding + $nav-padding + $nav-padding + $nav-indent;
  font-size: 12px;
}
```

Additionally, you'll also likely want to make another change in this same file to keep code examples on the same level as their appropriate explanations. This change needed would be located on line 350 at the time of writing.
```CSS
// the div is the tocify hidden div for placeholding stuff
& > h1,
& > h2,
& > h3,
& > h4,
& > div {
  clear: both;
}
```

Additionally, you'll also likely want to make another change in this same file to maintain good formatting of the TOC, This change needs to be added above line 375 at the time of writing.
```CSS
  h3 {
    @extend %header-font;
    font-size: 16px;
    margin-top: 0.5em;
    margin-bottom: 0;
    padding-top: 1.2em;
    padding-bottom: 1.2em;
    background-image: linear-gradient(to bottom, rgba(#fff, 0.2), rgba(#fff, 0));
  }

  h4 {
    @extend %header-font;
    font-size: 13px;
    margin-top: 0.5em;
    margin-bottom: 0;
    padding-top: 1.2em;
    padding-bottom: 1.2em;
    background-image: linear-gradient(to bottom, rgba(#fff, 0.2), rgba(#fff, 0));
  }
```

You will also need to change the following starting at line 375
```CSS
h3, h4, h5, h6 {
  @extend %header-font;
  font-size: 15px;
  margin-top: 2.5em;
  margin-bottom: 0.8em;
}
h4, h5, h6 {
  font-size: 10px;
}
```
To
```CSS
h5, h6 {
  @extend %header-font;
  font-size: 15px;
  margin-top: 2.5em;
  margin-bottom: 0.8em;
}
h5, h6 {
  font-size: 10px;
}
```

You'll also need to make a small change in `source/layouts/layout.erb`. The change needed would be located on line 80 at the time of writing. Add the following, immediately below the line ending in `<%= h2[:content] %></a>`:
```ruby
<% if h2[:children].length > 0 %>
  <ul class="toc-list-h3">
    <% h2[:children].each do |h3| %>
      <li>
        <a href="#<%= h3[:id] %>" class="toc-h3 toc-link" data-title="<%= h3[:content] %>"><%= h3[:content] %></a>
        <% if h3[:children].length > 0 %>
          <ul class="toc-list-h4">
            <% h3[:children].each do |h4| %>
              <li>
                <a href="#<%= h4[:id] %>" class="toc-h4 toc-link" data-title="<%= h4[:content] %>"><%= h4[:content] %></a>
              </li>
            <% end %>
          </ul>
        <% end %>
      </li>
    <% end %>
  </ul>
<% end %>
```

You'll also need to open `lib/toc_data.rb`,look at line 8 and line 18, add the new nest level to it, just like:
```ruby
html_doc.css('h1, h2, h3, h4, h5').each do |header|
```
and:
```ruby
  [5,4,3,2].each do |header_level|
```

Finally, to support searing in the new nesting levels, you should open `source/javascripts/app/_search.js`, look at line 23 and line 25, add the new nest levels to it, just like:
```javascript
$('h1, h2, h3, h4').each(function() {
```
and:
```javascript
var body = title.nextUntil('h1, h2, h3, h4');
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