### How the Language Tabs Work

The "language tabs" are the tabs that appear in the upper right of Slate. Users browsing the docs use them to select their programming language of choice.

In the Markdown file, you can use named code blocks to show the right programming language at the right time. For instance, if your page has `python` and `ruby` tabs, you can put this in your Markdown:

    ```ruby
    # This is some Ruby
    ```
    
    ```python
    # This is some Python
    ```

When the "ruby" tab is selected, only the Ruby code will show, and when the "python" tab is selected, only the Python code will show. It even has syntax highlighting if you give your code block one of the [names supported by Rouge](http://rouge.jayferd.us/demo)!

To edit the tabs, edit the `language-tabs` list at the top of `index.md`.

### Disabling the Language Tabs

If you don't want to use the language tabs, just delete the entire `languages-tabs` list from `index.md`, and then they'll disappear entirely from the page, making all code blocks always visible.

### Language Tab Display Names

The language name that you use next to the code blocks must exactly match one of the [Rouge supported languages](http://rouge.jayferd.us/demo). However, sometimes you want the language tab to list something else. For instance, you may want the `shell` language to appear in the language tab as "Curl".

Let's say your language tabs are like this:

    language_tabs:
      - shell
      - ruby
      - python

You want the "shell" to say "cURL" instead. You can't just change all instances of `shell` to `cURL`, since the [syntax highlighter](http://rouge.jayferd.us/demo) has no idea to highlight `cURL` like a shell script. Instead, just change your `language_tabs` to look like this:

    language_tabs:
      - shell: cURL
      - ruby
      - python

You continue using `shell` next to your code blocks, but the language tab now reads "cURL". You can also use this to make your language tabs have nicer capitalization:

    language_tabs:
      - shell: cURL
      - ruby: Ruby
      - python: Python

### Always-visible Code Blocks

If a language is not found in `language-tabs`, we'll *always* display it, no matter which language tab is selected. For instance, if your language tabs look like this:

    language_tabs:
      - shell
      - ruby

And you have code in your markdown that looks like this:

```markdown
    ```shell
    echo "hello world"
    ```

    ```ruby
    puts "hello world"
    ```

    ```json
    {
      "hello":"world"
    }
    ```
```

Then the JSON will *always* be visible, since JSON isn't one of the language tabs.