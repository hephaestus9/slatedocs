Slate supports specifying [`<meta>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta) tags to the site by modifying your index's YAML front matter. Here, you can specify a `meta` key, and underneath a list of dictionaries to define the meta tags to be included in your site.

For example, if you wanted to add a description and keywords meta tags, you would include the following:

```yaml
meta:
  - name: description
    content: Documentation for the Kittn API
  - name: keywords
    content: Kittn,API,Documentation
```

An example of usage can be seen [here](https://raw.githubusercontent.com/slatedocs/slate/8a5877f7c8b671e79496091fbdc9282f7983d234/source/index.html.md).

Please note, slate automatically sets the following meta tags:

* `<meta charset="utf-8">`
* `<meta content="IE=edge,chrome=1" http-equiv="X-UA-Compatible">`
* `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">`

If you wish to change these, you will need to modify the [`source/layouts/layout.erb`](https://github.com/slatedocs/slate/blob/main/source/layouts/layout.erb) file.