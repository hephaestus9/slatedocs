# How to add variables?

Mandatory for using variable tags in slate is that you change all `.md` files to `.md.erb`. You folder structure can look like:

    source/
        index.html.md.erb
    includes/
        _want-to-use-var.md.erb
    
Do not forget to change the include section in the index file. And yes, you can ignore the `_` from the include file. Slate needs this only for parsing.

```
includes:
 - want-to-use-var.md.erb
```

In `config.rb` create yourself a new section e.g. Global Variables and add the following lines.

```
# Global Variables
set :endpoint, 'https://my.endpoint.com'
config[:endpoint]
```

You have now created a global variables which you can use in your files with the following tag

```
<%= config[:endpoint] %>
```

An example for using variables could look like this:
```
Hello you want to access <%= config[:endpoint] %> !
```