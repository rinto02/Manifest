[BaikalOS Project](http://baikalos.ru)
====================================


Download the Source
===================

Please read the [AOSP building instructions](https://source.android.com/source/index.html) before proceeding.

Initializing Repository
-----------------------

Repo initialization:

    $ repo init --depth=1 -u https://github.com/Rint02/manifest.git -b r11.1


sync repo :

    $ repo sync

Some info on how to customize your sync:

  -f, --force-broken    continue sync even if a project fails to sync

  --force-sync          overwrite an existing git directory if it needs to
                        point to a different object directory. WARNING: this
                        may cause loss of data

  -l, --local-only      only update working tree, don't fetch

  -n, --network-only    fetch only, don't update working tree

  -c, --current-branch  fetch only current branch from server

  -j JOBS, --jobs=JOBS  projects to fetch simultaneously (default 4)

  --no-clone-bundle     disable use of /clone.bundle on HTTP/HTTPS

  --no-tags             don't fetch tags

Smallest/fastest sync:

    $ repo sync --no-tags --no-clone-bundle

    Note: we already define -c in our default.xml, so no need to add it

***

Building
--------

After the sync is finished, please read the [instructions from the Android site](https://source.android.com/source/building.html) on how to build.

    . build/envsetup.sh
    brunch


You can also build (and see how long it took) for specific devices like this:

    . build/envsetup.sh
    time brunch angler

Remember to `make clobber` every now and then!


Optional After Successful Build
--------------------------------

After you get a working build, and if you would like to share your build on XDA (Regular Unofficial Builds), then please use the following template to create
an XDA thread. Note that the template is a guideline of sort. You may make your own changes to it (especially please change the download link), but try
to stick as close as possible to the template. This is to avoid cluttering and make stuff organized.

Link : https://raw.githubusercontent.com/BaikalOS/vendor_baikalos/r11.1/docs/xda_template/xda_thread-template.txt


Uploading to baikalos Gerrit
---------------

1st You must have local ssh keys on your computer if you do not here is a [guide](https://help.github.com/articles/connecting-to-github-with-ssh/) to generate them

2nd Make an account on [Gerrit](http://gerrit.baikalos.ru) login only using GoogleAuth2

3rd Add your ssh public key to your account

4th Make your changes and commit them

5th use the following command to push your commit to gerrit

    (From root android directory)
    . build/envsetup.sh
    repo start r11.1 path/to/project
    cd path/to/project
    repo upload .

For more help on using this tool, use this command:

    repo help upload

You can also use:

    git push ssh://USERNAME@gerrit.baikalos.ru:29418/BaikalOS/REPO_NAME HEAD:refs/for/branch-name

Example:

    git push ssh://USERNAME@gerrit.baikalos.ru:29418/BaikalOS/manifest HEAD:refs/for/r11.1


6th You will get an error about a missing Change-ID in that error it will show you a suggested commit message copy the change id

7th Do the following command and add the Change-ID to the end of the commit message

    git commit --amend

Here is an example of what the commit message should look like:

> Add how to push to gerrit
>
> Change-Id: I93949d30d732de35222d9d78d1f94e33e4bffc47

8th use the same command to push to gerrit and if you did everything properly it will be up on gerrit



## Maintaining Authorship ##
Always make sure if you submit a patch/fix that you maintain authorship.
This is very important to not only us but to the entire open source community. It's what keeps it going and encourages more developers to contribute their work.

If you manually cherry pick a patch/fix add the original author prior to pushing to our gerrit.
This task is very easy and is usually done after you commit a patch/fix locally.

i.e - Once you type in "git commit -a" the commit message and you have saved it, type in the following:

```bash
git commit --amend --author "Author <email@address.com>"
```

So it should look like this once you get all author's information:

```bash
git commit --amend --author "John Doe <john.doe@gmail.com>"
```

Picking changes from our gerrit
-------------------------------

(From root android directory)
    . build/envsetup.sh

to pick every change from a topic:

    repopick -t topic

to pick a specific change

    repopick commit-number

example, to pick this commit: https://gerrit.baikalos.ru/#/c/36939/

    repopick 36939


Additonal build info
-------------------------------
https://github.com/BaikalOS/vendor_baikalos/blob/r11.1/docs/baikalosInfo.md


## Maintainer Application ##
If you have the necessary skills and would like to become a part of our group by becoming a maintainer,
please see [this link](https://github.com/BaikalOS/vendor_baikalos/blob/r11.1/docs/maintainerApplication.md) for further information and maintainer application.
