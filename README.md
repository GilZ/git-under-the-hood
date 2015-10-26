Git Under The Hood
==================
________________________________________________

What are we going to talk about
-------------------------------

1. Short intro - what does "under the hood" mean?
1. What is a branch (and how to create one using a text editor)
1. What is a commit
1. What is HEAD (and how to checkout using a text editor)
1. Merge strategies (or what is the difference between --rebase and --no-ff)
1. Working with remote repository (or what is the difference between origin master and origin/master)
1. Git flow
1. Git hooks, .gitignore and aliases (if time will allow)

________________________________________________

What aren't we going to talk about
----------------------------------
* Working with Source Tree or any other tool
* The meaning of the command:
```bash
git log -i -E -5 -F --no-min-parents --all -g --pretty=format:"%cd %cn %ci %T %ai"
```
(or: RTFM)

________________________________________________

What is a branch?
-----------------

* A branch is just a pointer to a commit
* It is saved as a file in the .git/refs/heads folder
* Demo: create a new branch using a text editor
```bash
vi .git/refs/heads/my-branch
```

________________________________________________

What is a commit?
-----------------
* TODO

________________________________________________

What is HEAD?
-------------

* HEAD is a reference to the last commit in the current checked out branch.
 * Usually, you can think of i as a soft link to the last commit:
```bash
cat .git/HEAD
```
* Sometimes (e.g. when you have conflict, or when you checkout a commit instead of a branch, you'll be in *detached HEAD state*
 * It just means that HEAD is now pointing to a commit, not a branch
* Demo: checkout using a text editor
```bash
vi .git/HEAD
```

