### How do I add programming languages to the tabs in the upper right corner?

At the top of `index.md`, just add more languages to the list under `language-tabs`.

Note that if a language is not found in `language-tabs`, we'll *always* display it. For instance, if your language tabs look like this:

    language_tabs:
      - shell
      - ruby

And you have code in your markdown that looks like this:

```
	```ruby
	# This is some Ruby code!
	```

	```python
	// This is some Python code!
	```
```

Then the JSON will *always* be visible, since JSON isn't one of the language tabs.