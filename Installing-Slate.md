### Prerequisites

You're going to need:

 - **Linux or macOS** — Windows may work, but is unsupported. For OSX, see [installing_nokogiri](https://github.com/sparklemotion/nokogiri.org-tutorials/blob/master/content/installing_nokogiri.md) prior to getting started
 - **Ruby, version 2.2.5 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
3. `cd slate`
4. Initialize and start Slate. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567. Whoa! That was fast!

### What Now?

The next step is to [learn how to edit `source/index.md` to change the content of your docs](Markdown-Syntax).