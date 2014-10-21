# Custom Domain

Follow [this guide](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/) to set up a custom domain for your Slate build published on GitHub Pages (github.io).  

It's important to note that the `CNAME` file should not be placed into the root of your repository.  Instead, place the CNAME file into the `/source/` directory, and when you `rake publish`, it will automatically be placed into the root of the `gh-pages` branch.