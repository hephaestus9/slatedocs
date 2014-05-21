If you want to break your `index.md` into multiple files, use includes!

Each entry in the `includes` list at the top of `index.md` refers to a file in the `includes` directory, like this:

    includes:
      - api/databases

Will append the content of `includes/api/_databases.md` to the end of `index.md`. Note the underscore in the filename, and how it isn't necessary in the list entry.