With a small change you can embed small bits of ruby code in your Markdown.

This may be helpful to generate parts of your Markdown code.

Add this method to "unique_head.rb", which is the renderer class for Redcarpet.

```
  def preprocess(full_document)
    full_document = super(full_document) if defined?(super)
    full_document = ERB.new(full_document).result(binding)
    return full_document
  end

```

Now you can embed ERB code in markdown just like ERB in html.

```
<%= 1 + 1 %>
```

Any methods or variables visible in the class where "preprocess" is defined can be called from within ERB. 