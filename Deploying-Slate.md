Slate spits out a bunch of static HTML, Javascript, and CSS, so it's pretty trivial to host.

### Publishing Your Docs to Github Pages

Publishing your API documentation couldn't be more simple.

 1. Make sure your `origin` is a Slate fork in your own account, not our original repo.
 1. Commit your changes to the markdown source: `git commit -a -m "Update index.md"`
 2. Push the *markdown source* changes to Github: `git push`
 3. Run `./deploy.sh`

Done! Your changes should now be live on http://yourusername.github.io/slate, and the main branch should be updated with your edited markdown. Note that if this is your first time publishing Slate, it can sometimes take ten minutes or so before your content is available online.

Also, thanks to [X1011](https://github.com/X1011/git-directory-deploy) for the excellent deploy script.

### Publishing Your Docs to Your Own Server

Instead of using `rake publish`, use `rake build`. Middleman will build your website to the `build` directory of your project, and you can copy those static HTML files to the server of your choice.

Another alternative is to use the [middleman-deploy](https://github.com/middleman-contrib/middleman-deploy) gem. 

### Custom Domains with Github

If you're hosting Slate with Github Pages, setting up a custom domain name is simple! Just follow the instructions [in Github's help center](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/). Note that instead of putting the `CNAME` file in the root directory of your Slate, you should put it in the `source` folder. When Middleman publishes to the `gh-pages` branch, it will copy it to the root folder of that branch.