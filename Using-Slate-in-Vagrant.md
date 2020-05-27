Provided in the slate repo is a Vagrantfile you can use to run slate using [vagrant](https://www.vagrantup.com/). Vagrant is used to create a virtual machine (VM) that runs under VirtualBox or other related software and provides you a reproducible and portable development environment, without having to figure things out on your host. This is especially useful for Windows where getting things right, like nokogiri which potentially requires native compilation, can be tricky.

## Dependencies

* [Vagrant](https://www.vagrantup.com/), see [this page](https://www.vagrantup.com/downloads.html) for installation downloads
* [VirtualBox](https://www.virtualbox.org/), see [this page](https://www.virtualbox.org/wiki/Downloads) for installation downloads

## Getting started

1. Fork this repository on Github.
2. Clone *your forked repository* (not our original one) to your hard drive with `git clone https://github.com/YOURUSERNAME/slate.git`
3. `cd slate`

## Running Vagrant

Creating the Vagrant VM is as easy as doing:

```bash
vagrant up
```

And you can view your docs at http://localhost:4567.

If you wish to build the docs to HTML, run

```bash
vagrant ssh -c "cd /vagrant; bundle exec middleman build"
```

## Stopping Vagrant

Once your done with your work and you wish to shutdown the VM that vagrant creates, you will need to run:

```bash
vagrant halt
```

## What Now?

The next step is to [learn how to edit `source/index.md` to change the content of your docs](Markdown-Syntax). Once your done, you might want to think about [deploying your docs](https://github.com/slatedocs/slate/wiki/Deploying-Slate).