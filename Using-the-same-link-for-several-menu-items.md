If you have several menu items with the same name, only the first link will work. Nevertheless it is possible to use links with the same name. 

## Configuration

For this you have to make the following adjustments in the config.rb file: 

1. Replace the standard require with the following code

```ruby
# Unique header generation
require './lib/nesting_unique_head.rb'
```

2. Adjust the markdown renderer

```ruby
# Markdown
set :markdown_engine, :redcarpet
set :markdown,

    # some more config here

    renderer: NestingUniqueHeadCounter
```

## Result

This change will nest your links under your h1 Titles. Let's say you have the following structure:

```
# (H1) Accounts
## (H2) Authentication

# (H1) Requests
## (H2) Authentication
```

Both authentication links will work now by creating the following anchor links:

```
#accounts
#accounts-authentication

#requests
#requests-authentication
```


