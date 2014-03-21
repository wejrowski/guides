Feature Workflow
================

Create Branch
-------------

Create a local feature branch

* For patches (work that needs to be sent to production before next release)
  * branch off master, send pull-request to patch
* For normal features and bugs
  * branch off release & send pull-request to release

```
git checkout release
git pull
git checkout -b <branch-name>
```

Write and commit code
---------------------

Rebase frequently to incorporate upstream changes.

    git fetch origin
    git rebase origin/release

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    rake
    git add --all

When you've staged the changes, commit them.

    git status
    git commit --verbose

Write a [good commit message]. Example format:

    Present-tense summary under 50 characters

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    http:://project.management-system.com/ticket/123

Share your branch
-----------------

Share and submit a [GitHub pull request].

    git push origin <branch-name>
    git pull-request -b <upstream-account>:<branch-name> -h <my-account>:<branch-name>

Write a great pull request message:

    Simple title

    http:://project.management-system.com/ticket/123

    - [ ] Tests pass
    - [ ] QA passed

    Other relevant info, or reflections/questions for everyone

Ask for a code review in HipChat.

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[GitHub pull request]: https://help.github.com/articles/using-pull-requests/

Review code
-----------

A team member other than the author reviews the pull request. They follow
[Code Review](../code-review) guidelines to avoid
miscommunication.

They make comments and ask questions directly on lines of code in the Github
web interface or in HipChat.

For changes which they can make themselves, they check out the branch.

    git checkout <branch-name>
    rake db:migrate
    rake
    git diff staging/master..HEAD

They make small changes right in the branch, test the feature in browser,
run tests, commit, and push.

When satisfied, they comment on the pull request `Ready to merge.`

Merge
-----

View a list of new commits. View changed files. Merge branch into master.

    git log origin/master..<branch-name>
    git diff --stat origin/master
    git checkout master
    git merge <branch-name> --ff-only
    git push

Delete your remote feature branch.

    git push origin --delete <branch-name>

Delete your local feature branch.

    git branch --delete <branch-name>
