> I get the error:
> ```
> Input.error ((execjs):58303:16): CssSyntaxError: /stylesheets/screen.css:5:1: Unknown word (ExecJS::RuntimeError)
> 
>   3 | @import 'variables';
>   4 | @import 'icon-font';
> > 5 | // uncomment to switch to RTL format
>     | ^
>   6 | // @import 'rtl';
>   7 |
>```

This is because Slate is attempting to use the sassc gem to compile the scss stylesheets. You need to make sure you are using the `sass` gem. You can accomplish this by making sure the `sass` gem is in your `Gemfile` and that `middleman-sprockets` is on `~>3`, and not using `~>4`.

----

> I get an error that says `WARNING: V8 isolate was forked, it can not be disposed and memory will not be reclaimed till the Ruby process exits.` and attempting to build hangs / fails.

This generally means you're attempting to use `mini_racer` as was recommended in older versions of Slate. This gem has issues working properly with Slate, and it is recommended that you just install [Node.js](https://nodejs.org/en/) runtime and remove `mini_racer` from your `Gemfile`.