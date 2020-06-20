Add the remote, call it `upstream`:

    git remote add upstream https://github.com/slatedocs/slate.git

Fetch all the branches of that remote into remote-tracking branches, such as `upstream/main`:

    git fetch upstream

Make sure that you're on _your_ main branch:

    git checkout main

Merge _our_ updates into your main branch:

    git merge upstream/main

Push the updated code to Github:

    git push

Update installed gems (if using slate natively):

    bundle install

Publish the new changes to Github pages:

    ./deploy.sh

(Thanks to [Mark Longair on StackOverflow](http://stackoverflow.com/questions/7244321/how-to-update-github-forked-repository) for the upstream explanation.)

If using Slate under Vagrant or Docker, you will want to destroy and rebuild the Slate image for it, using either `vagrant destroy` or `docker rmi slate` while in the slate directory, and then re-running through the instructions on those pages.