### Prerequisites

You're going to need:

 - **Linux or macOS** — Windows may work, but is unsupported. For OSX and Ubuntu see [installing_nokogiri](https://github.com/sparklemotion/nokogiri.org-tutorials/blob/master/content/installing_nokogiri.md) prior to getting started
 - **Ruby, version 2.2.5 or newer**
 - **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.
- **npm**

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

### Possible issues

If you struggling from error message like in ([#1003](https://github.com/lord/slate/issues/1003))
```
...
autodetect: Could not find a JavaScript runtime
...
```

Then you need to install JavaScript runtime for your machine / docker environment. Follow the instructions on  [NodeJS](https://nodejs.org/en/download) website. For example:

Linux:
```
apt-get install nodejs
```

macOS (for [Brew](https://brew.sh/) users):
```
brew install node
```

StackOverflow question: [ExecJS and could not find a JavaScript runtime](https://stackoverflow.com/questions/6282307/execjs-and-could-not-find-a-javascript-runtime)

### What Now?

The next step is to [learn how to edit `source/index.md` to change the content of your docs](Markdown-Syntax).