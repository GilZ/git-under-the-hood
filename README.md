Git Under The Hood
==================
![XKCD](http://imgs.xkcd.com/comics/git.png)

If that doesn't fix it, git.txt contains the phone number of a friend of mine who understands git. Just wait through a few minutes of 'It's really pretty simple, just think of branches as...' and eventually you'll learn the commands that will fix everything.

---

What are we going to talk about
-------------------------------

1. *Short intro* - what does "under the hood" mean?
1. *What is a branch* (and how to create one using a text editor)
1. *What is a commit*
1. *What is HEAD* (and how to checkout using a text editor)
1. *Merge techniques* (or what is the difference between --rebase and --no-ff)
1. *Working with remote repositories* (or what is the difference between origin master and origin/master)
1. *Git flow*
1. *Git hooks, .gitignore and aliases* (if time will allow)

---

What aren't we going to talk about
----------------------------------
* Working with Source Tree or any other tool
* The meaning of the command: `git log -i -E -5 -F --no-min-parents --all -g --pretty=format:"%cd %cn %ci %T %ai"` (or: RTFM)

---

What is a branch?
-----------------

* A branch is just a pointer to a commit
* It is saved as a file in the .git/refs/heads folder
* Demo: create a new branch using a text editor
`vi .git/refs/heads/my-branch`

---


What is a commit?
-----------------
* TODO

---


What is HEAD?
-------------

* HEAD is a reference to the last commit in the current checked out branch.
 * Usually, you can think of i as a soft link to the last commit:
    `cat .git/HEAD`
* Sometimes (e.g. when you have conflict, or when you checkout a commit instead of a branch, you'll be in *detached HEAD state*
 * It just means that HEAD is now pointing to a commit, not a branch
* Demo: checkout using a text editor `vi .git/HEAD`


---


Merge techniques
----------------

* There are 3 (major) merge techniques in git: *fast forward*, *no fast forward* and *rebase*.

---

1. *Fast forward*: This is the default technique. Try to add the merged sub tree as commits on top of the existing commits:
`echo "master" > master.txt && git add --all && git commit -am "Commit example 1"`
`git checkout -b ff-branch && echo "ff" > ff.txt && git add --all && git commit -am "Commit example 2"`
`git merge ff-branch && git l`

---

2. *No fast forward*: This method will force git to create a merge commit - A commit with 2 (or more) parents:
`echo "master" > master2.txt && git add --all && git commit -am "Commit example 4"`
`git checkout -b noff-branch && echo "noff" > noff.txt && git add --all && git commit -am "Commit example 5"`
`git checkout master && echo "master" >> master2.txt && git add --all && git commit -am "Commit example 6"`
`git merge --no-ff noff-branch && git l`

---

3. *Rebase* When using rebase, the changed from the other branch are _fast-forwarded_, and afterwards the changed from the current branched are _replayed_ one by one
`echo "master" > master3.txt && git add --all && git commit -am "Commit example 7"`
`git checkout -b rebase-branch && echo "rebase" > rebase.txt && git add --all && git commit -am "Commit example 8"`
`git checkout master && echo "master" >> master3.txt && git add --all && git commit -am "Commit example 9"`
`git rebase rebase-branch && git l`

---

Working with remote repositories
--------------------------------

* Git is a distributed SCM, and doesn't need a central server.
* Commands that communicate with a remote host (e.g. `pull`, `push`, `fetch`, etc.) can get a host name as a parameter
 * We can think of it like a dialog: `git pull origin master`
  - Hi `git`
  - *What?*
  - `pull`
  - *From where?*
  - From `origin`
  - *What should I `pull`?*
  - `master`
  - *OK*

---

Working with remote repositories (cont.)
----------------------------------------

* Some commands update local copies of the remote references: `cat .git/refs/remotes/origin/master`
* Commands that can work on references (e.g. `merge`, `log`, `checkout`, etc.) can use these references like any other
 * Again, we can think of it like a dialog: `git merge origin/master`
  - Hi `git`
  - *What?*
  - `merge`
  - *From where?*
  - From `origin/master`
  - *OK*
  - Thank you
  - *You're welcome*

---

Working with remote repositories (cont.)
----------------------------------------

* As mentioned earlier, git allows us to work with more than one remote server
* School example: Bob is the remote for Alice, Alice is the remote for Charlie and Eve
* Real world example: working on an open source project:
 * Fork the original repository in GitHub
 * Clone a local copy of your repository
 * Commit and push to your repository, but pull from the original repository to keep it up-to-date

---

Git flow
--------
http://nvie.com/img/git-model@2x.png

---

Aliases
-------
[My gitconfig file with all my cool aliases](./.gitconfig)


