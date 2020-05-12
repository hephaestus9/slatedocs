To make basic changes to the sizes, padding, and colors, you can edit
[`source/stylesheets/_variables.scss`](https://github.com/slatedocs/slate/blob/master/source/stylesheets/_variables.scss).
If you don't need to make any major changes, this is the preferred way to edit Slate, since it makes updating Slate a
little easier.

If you want to make more significant changes to Slate's overall look and feel, feel free to dive into 
[`source/stylesheets/screen.css.scss`](https://github.com/slatedocs/slate/blob/master/source/stylesheets/screen.css.scss)
and
[`source/stylesheets/print.css.scss`](https://github.com/slatedocs/slate/blob/master/source/stylesheets/print.css.scss)
(the print stylesheet). They're fairly well documented and organized, but if you need some help, feel free to submit an
issue.

If you wish to modify the styling of code highlighting, while you can modify the above SCSS files and include rules,
you will have a much easier time by modifying the Slate Rouge theme, using a different builtin Rouge theme, or
by creating your own. You can modify the theme Slate uses by diving into
[`lib/monokai_sublime_slate.rb`](https://github.com/slatedocs/slate/blob/master/lib/monokai_sublime_slate.rb),
which is an extension off the Rouge MonokaiSublime theme. Alternatively, if you wish to use a different Rouge
theme, you will want to edit
[`source/layouts/layout.erb`](https://github.com/slatedocs/slate/blob/master/source/layouts/layout.erb) and modify this
line to point to the theme you want:

```erb
      <%= Rouge::Themes::MonokaiSublimeSlate.render(:scope => '.highlight') %>
```

A full list of available builtin Rouge themes can be found [here](https://github.com/rouge-ruby/rouge/tree/master/lib/rouge/themes).
You can also see the list of available tokens you can style [here](https://github.com/rouge-ruby/rouge/wiki/List-of-tokens).

## Other People's Slate Theming:
 
Some people have done some cool heavy styling on their Slate pages — you can take a look at their Slate sources
below:

- [TradeGecko](https://github.com/tradegecko/smaug/)
