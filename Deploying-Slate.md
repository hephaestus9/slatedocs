Slate spits out a bunch of static HTML, Javascript, and CSS, so it's pretty trivial to host.

### Publishing Your Docs to GitHub Pages

Publishing your API documentation couldn't be more simple.

 1. Make sure you're working on a fork in your own account, not our original repo: `git remote show origin`.
 1. Commit your changes to the markdown source: `git commit -a -m "Update index.md"`
 2. Push the *markdown source* changes to GitHub: `git push`
 3. Run `./deploy.sh`

NOTE: Using the git way, you should not make changes to your repo on github.com for example.

NOTE: For automated publishing using CI, please see below.

NOTE: If using Docker, you will want to run `./deploy.sh --push-only` as the final step.

Done! Your changes should now be live on http://yourusername.github.io/slate, and the main branch should be updated with your edited markdown. Note that if this is your first time publishing Slate, it can sometimes take ten minutes or so before your content is available online. It can also take a moment even if it's not the first time. 

Also, thanks to [X1011](https://github.com/X1011/git-directory-deploy) for the excellent deploy script.

### Publishing Your Docs to Your Own Server

Do not, I repeat, **do not run Middleman on your production server**. Middleman is not designed to be secure on a public server. It is not designed to load pages quickly. It is *purely* for development.

You can publish *static* documents to your own server using ```bundle exec middleman build --clean```. Middleman will build your website to the `build` directory of your project, and you can copy those static HTML files to the server of your choice. Since you're just copying static files over, you don't need to run Middleman on your server.

Another alternative is to use the [middleman-deploy](https://github.com/middleman-contrib/middleman-deploy) gem.

### Custom Domains with GitHub

If you're hosting Slate with GitHub Pages, setting up a custom domain name is simple! Just follow the instructions [in GitHub's help center](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/). Note that instead of putting the `CNAME` file in the root directory of your Slate, you should put it in the `source` folder. When Middleman publishes to the `gh-pages` branch, it will copy it to the root folder of that branch.

Unfortunately, the deploy system will overwrite any custom domain name you've set within GitHub settings. This isn't something we can easily fix — it's a quirk with how GitHub handles custom domains. So until they fix it, use the `CNAME` file instead!

### Publishing using Travis-CI

To use [Travis-CI](https://travis-ci.com/) to publish slate to your gh-pages, it is recommend to not use the `./deploy.sh` script directly, but rather just do `./deploy.sh --source-only` and then use their [built-in GitHub pages deployment](https://docs.travis-ci.com/user/deployment/pages/). 

NOTE: If you use `./deploy.sh` directly on Travis-CI, if the script fails for whatever reason, your git credentials may leak.

An example .travis.yml file for deploying base slate:

```yaml
language: ruby
cache: bundler

rvm:
  - 2.5.3

before_install:
  - gem update --system
  - gem install bundler

script:
  - ./deploy.sh --source-only

deploy:
  provider: pages
  local_dir: build/
  skip_cleanup: true
  # see https://docs.travis-ci.com/user/deployment/pages/#setting-the-github-token
  github_token: $GITHUB_TOKEN
  keep_history: true
  target_branch: gh-pages
  on:
    branch: master
```

### Publishing using GitHub Actions

To use [GitHub Actions](https://github.com/features/actions) to publish slate to your gh-pages, please see how Slate itself [uses it](https://github.com/slatedocs/slate/blob/main/.github/workflows/deploy.yml) to publish its demo site. By default, when you create repository from this one, your site will automatically be set-up to use this workflow.