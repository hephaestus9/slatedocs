Add the remote, call it `upstream`:

    git remote add upstream https://github.com/lord/slate.git

Fetch all the branches of that remote into remote-tracking branches, such as `upstream/master`:

    git fetch upstream

Make sure that you're on _your_ master branch:

    git checkout master

Merge _our_ updates into your master branch:

    git merge upstream/master

Push the updated code to Github:

    git push

Publish the new changes to Github pages:

    ./deploy.sh

(Thanks to [Mark Longair on StackOverflow](http://stackoverflow.com/questions/7244321/how-to-update-github-forked-repository) for the upstream explanation.)