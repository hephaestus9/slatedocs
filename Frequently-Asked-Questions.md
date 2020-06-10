1. I get the error:
```
Input.error ((execjs):58303:16): CssSyntaxError: /stylesheets/screen.css:5:1: Unknown word (ExecJS::RuntimeError)

  3 | @import 'variables';
  4 | @import 'icon-font';
> 5 | // uncomment to switch to RTL format
    | ^
  6 | // @import 'rtl';
  7 |
```

This is because Slate is attempting to use the sassc gem to compile the scss stylesheets. You need to make sure you are using the `sass` gem. You can accomplish this by making sure the `sass` gem is in your `Gemfile` and that `middleman-sprockets` is on `~>3`, and not using `~>4`.