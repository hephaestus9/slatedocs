# Global Includes
If you want to break your `index.md` into multiple files, use includes!

Each entry in the `includes` list at the top of `index.md` refers to a file in the `includes` directory, like this:

    includes:
      - api/databases

Will append the content of `includes/api/_databases.md` to the end of `index.md`. Note that the (required) underscore in the filename isn't in the list entry.

# Partial Includes
When your api reaches a certain size where you cannot avoid referencing certain text blocks from previous section, then you can use partial includes.

In order to use partials. We need to modify the folder structure of slate. First we need to change `index.html.md` to `index.html.md.erb`.

Next we need create a new file which contains are text block e.g. `test_partial.md.erb`.

The folder structure should now look like:

    source/
        index.html.md.erb
    source/includes
        test_partial.md.erb

Now we want to add a partial tag in `index.html.md.erb` in order to reference to our repetitive text blocks.
We do this with adding following line: `<%= partial "includes/test_partial.md.erb" %>`
