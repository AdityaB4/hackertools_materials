- A **version control system (VCS)** helps to record changes to a file or a set of files over time
- It allows you to revert a project to a previous state, or to compare changes over time
- Acts as an "undo" button for your code and lets your collaborate with your team
- Created by Linus Torvalds in 2005 as a replacement for existing VCS for the Linux kernel
- A distributed version control system (DVCS)
- Every commit is a *snapshot* of your files
- GitHub != Git
<!-- TODO: Delete if needed -->
<!-- TODO: See how to explain this concisely -->
- Working directory: where you actually work
- Index/\"staging\" area: where you construct a commit
- Repository/commit: the repository itself
```
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Now, we will create a new repository for this session.
## Creating a new GitHub repository

<!-- TODO: Use new image -->
![](github-new.png)

---

## Creating a new GitHub repository

<!-- TODO: Use new image -->
![](github-new-2.png)

---

## Creating a new GitHub repository

<!-- TODO: Use new image -->
![](github-new-3.png){style="height: 22ex;"}

## Cloning the repository

Downloading a local copy of the repository

```bash
git clone https://github.com/<your GitHub username>/learning-git.git
```

The server (i.e. GitHub) stores the remote copy (like a single source of truth)

<!-- TODO: Explain what [origin] means -->

<!-- TODO: Include pictures -->
![]()

---

<!-- TODO: If too much time spent, skip this -->
<!-- TODO: Maybe ignore -->
Create a new file in `hello.txt`, however you want. Then add it:

```
$ echo 'Hello world' > hello.txt
$ git add hello.txt
```
Staging tells Git that you want to include the file in your next snapshot.
```
```
```
On branch master
No commits yet
Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
    new file:   hello
```
Committing files is taking the snapshot of the files that have been staged.

```
```

```
[master (root-commit) 5d74ce3] Add hello
    1 file changed, 1 insertion(+)
    create mode 100644 hello
```
Make edits to `hello.txt` (or whatever file you made), then
```
```
```
diff --git a/hello b/hello
index 802992c..5d56d4d 100644
--- a/hello
+++ b/hello
@@ -1 +1 @@
-Hello world
+Hello Hackerschool!
```
`git diff` shows the changes to file content.
## Viewing commit history
```
$ git log
```
```
commit 19c32155172a20f2fd14fe0e6c0fea954c17296b (HEAD -> master)
Author: Your Name <your@email.com>
Date:   Sat May 8 21:36:58 2021 +0800
    Change world to Hackerschool!
commit dc37b1cb2627f9829db0072cfa7d3d6bf9eb6822
Author: Your Name <your@email.com>
Date:   Sat May 8 21:16:45 2021 +0800
    Add hello
```
<!-- TODO: Treat this section as both try it out and Q&A session -->
## Intermission
5 minutes...
In the meantime, try out the commands that you have learnt! Add new files, edit them,
commit them, and stage them!
## Collaborating with others
## Collaboration Workflows
1. Branch & PR
2. Fork & PR

This workshop focuses on the former - "Branch & PR"

::: { .font50 }

For more information about "Fork & PR", you [can visit this link here](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

:::

## What is a branch?
A branch is an independent line of development, often used for features or bug fixes
that should not be directly and immediately saved onto the main branch
![](./branch.svg)

Main branch is the initial and primary place where most development occurs (`main` is traditionally used but can be named anything, used to be known as `master` branch)

## HEAD

`HEAD` is a special name given to the current commit of your current branch for ease of reference

:::
## Why use branching?

::: {.font75}
:::

```
$ git checkout -b new-feature
Switched to a new branch 'new-feature'
```
```
$ git branch new-feature
$ git checkout new-feature
Switched to branch 'new-feature'
```
```
$ git branch
    main
* new-feature
```
```
$ git checkout main
Switched to branch 'main'
```
## Branch & PR Workflow
Each member owns their copy of the repository locally (through cloning)
When working on a new feature or bug fix, each member will
1. Pull the latest changes from the remote repository
2. Create a branch per feature/bug fix on their local copy
3. Edit the files in their respective branch
4. Push their local branch to the repository
5. Make a pull request of their feature/bug fix branch to the `main` branch (remote copy)
---
## Hands-on Time!
## Setup
Add your teammate as a collaborator to your newly created GitHub repository (Settings > Manage access > Invite a collaborator)
![](./collaborator.png)
Clone their repository onto your machine (name it something different from your own):
```
$ git clone https://github.com/<your teammate's GitHub name>/my-new-repo.git my-friend-repo/
$ cd my-friend-repo/
```
## Creating a branch
```
$ git checkout -b feature-1
```
## Making your changes
Edit your friend's `hello.txt` to have whatever content you want and then stage and commit the file:
```
$ git add hello.txt
$ git commit -m "Update hello.txt"
```
## Pushing local changes to the remote repository
```
$ git push origin feature-1
```
## Opening a pull request on the repository
Repository page > Pull Requests > New pull request
![](github-pr-1.png){style="height: 12ex"}
## Creating pull request
Ensure that the `compare` branch is your local feature branch and `base` branch
is `main` branch

<!-- TODO: Add updated screenshot -->
![](./pr-page.png)
## Creating pull request
Confirm pull request with "Create pull request"

<!-- TODO: Add updated screenshot -->
![](./pr-details.png)
## Reviewing pull requests
Your repository > Pull Requests > Select your friend's pull request
![](./view-pr.png)
View the commits and the files changed through the tabs.
## Accepting pull requests
If the files are in order, click "Merge pull request" to accept their changes into
your repository's `main` branch
---
## Getting latest remote copy on your local copy
```
git pull origin main
```
## Merging
<!-- TODO: Improve explanation -->
Combining your branch to `main` branch
![](./merge.png)
## Handling (merge) conflicts
Merge conflicts arise when the same line of code is changed across two commits
so there is a conflict in which to be used
---
## Simulating merge conflicts
In your repository, create branch `conflict-1` from `main` and edit the first line of `hello.txt`
```
$ git checkout -b conflict-1
```
Return to `main` and create another branch `conflict-2` from `main` and edit the first line of `hello.txt` again

```
$ git checkout main
$ git checkout -b conflict-2
```
## Merge conflicts

![](conflict-1.svg){.white-bg}
## Merge conflicts
Now, try to merge `conflict-1` and `conflict-2` into `main`.
```
$ git merge conflict-1
Updating b53e9cf..87a92c3
Fast-forward
    hello.txt | 2 +-
    1 file changed, 1 insertion(+), 1 deletion(-)
$ git merge conflict-2
Auto-merging hello.txt
CONFLICT (content): Merge conflict in hello.txt
Automatic merge failed; fix conflicts and then commit the result.
```
## Handling merge conflicts
```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
(use "git push" to publish your local commits)
You have unmerged paths.
(fix conflicts and run "git commit")
(use "git merge --abort" to abort the merge)
Unmerged paths:
(use "git add <file>..." to mark resolution)
both modified:   hello.txt
no changes added to commit (use "git add" and/or "git commit -a")
```
---
## Handling merge conflicts
```
$ cat hello.txt
<<<<<<< HEAD
Goodbye!
=======
Farewell!
>>>>>>> conflict-2
```
[What we have in `main`]{.mark}
[What we want to merge in `conflict-2`]{.mark-red}
## Handling merge conflicts
<!-- TODO: MUST DEMO TO EXPLAIN -->
Edit `hello.txt` as such...
---
## Handling merge conflicts
![](conflict-2.svg){.white-bg}
## Summary
-   [`git checkout`](https://git-scm.com/docs/git-checkout): Checkout a
    branch (and also files, etc)
-   [`git merge`](https://git-scm.com/docs/git-merge): Merge a branch
-   [`git clone`](https://git-scm.com/docs/git-clone): Clone a remote
    repository
-   [`git remote`](https://git-scm.com/docs/git-remote): Manage remotes
-   [`git push`](https://git-scm.com/docs/git-push): Push your branch to
    a remote
-   [`git pull`](https://git-scm.com/docs/git-pull): Pull updates from a
    remote to your repository
## Intermission!
5 minute break and Q&A!
---

## Additional Notes
<!-- TODO: Remove if too long -->
## Commit message discipline

First line: 80-character title, phrased imperatively

Then if your change is complex, elaborate on the change in prose.

``` font45
Change greeting from "Hi" to "Hello"

"Hi" is a bit too informal for a greeting. We should change it to "Hello" instead,
so that our users don't feel like we are being too informal. Blah blah blah blah.
Blah blah.
```

Undo accidental changes made
```
$ git log --graph --oneline
* d1f4fcc (HEAD -> master, origin/master, origin/HEAD) Add file3
* 643aec6 Update file to c
* 4ec21c7 Update file to b
* 055cab4 Initial commit
```
```
$ git revert 643aec6
[master 7b73baf] Revert "Update file to c"
    1 file changed, 1 insertion(+), 1 deletion(-)
$ git show
commit 7b73baf229e2b8db19bc594c450743b50adf649d (HEAD -> master)
Author: Your Name <your@email.com>
Date:   Tue May 11 01:21:31 2021 +0800
    Revert "Update file to c"
    This reverts commit 643aec6d2a1b4cd485d678886fc1cef25b15bee0.
diff --git a/file b/file
index f2ad6c7..6178079 100644
--- a/file
+++ b/file
@@ -1 +1 @@
-c
+b
```
```
$ echo e > file
$ git add file
$ git status
On branch master
Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
    modified:   file
$ git reset file
Unstaged changes after reset:
M   file
$ git status
On branch master
Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
    modified:   file
no changes added to commit (use "git add" and/or "git commit -a")
```
```
$ echo e > file
$ git status
On branch master
Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
    modified:   file

no changes added to commit (use "git add" and/or "git commit -a")
$ git checkout -- file
$ git status
On branch master
nothing to commit, working tree clean
```
## Summary
## Ignoring files
Sometimes we don\'t want Git to track a certain file
~~~ {.bash-strong}
$ touch ignore-me
$ git status
~~~
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
        ignore-me
    nothing added to commit but untracked files present (use "git add" to track)
## Ignoring files
We can add it to `.gitignore`
~~~ {.bash-strong}
$ echo "/ignore-me" >> .gitignore
$ git status
~~~
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
        .gitignore
    nothing added to commit but untracked files present (use "git add" to track)
`.gitignore` should be committed.
## Ignoring files
~~~ {.bash-strong}
$ git add .gitignore && git commit -m "Add .gitignore"
~~~
    [master 5ada1cf] Add .gitignore
     1 file changed, 1 insertion(+)
     create mode 100644 .gitignore
~~~ {.bash-strong}
$ git status
~~~
    On branch master
    nothing to commit, working tree clean
~~~ {.bash-strong}
$ git status --ignored
~~~
    On branch master
    Ignored files:
      (use "git add -f <file>..." to include in what will be committed)
        ignore-me
    nothing to commit, working tree clean
## What to ignore?
Typically, we ignore files like build artifacts and generated files that
are usually derived from the human-authored code in the repository. E.g.
-   dependency caches like `/node_modules`
-   compiled code like `.o`, `.pyc` files
-   build output directories like `/bin`, `/out`
-   runtime-generated files like log files
-   personal configuration files e.g. of your IDE
## `.gitignore` format
    /logs/*/*.log
    /logs/**/*.log
    **/logs
    **/logs/debug.log
    *.log
    /debug.log
    debug.log
[See the full pattern
format.](https://git-scm.com/docs/gitignore#_pattern_format)
Additional readings:
- [Git manual](https://git-scm.com/docs)
- [Pro Git](https://git-scm.com/book/en/v2)
- [NUS Hackers Git Cheatsheet](https://hckr.cc/ht-git-cs)
- Look into [Git
- If you're interested in how version control works with lots of technical details,
- GitHub isn't the only way you can share you repositories online! You could even self host your own Git servers.
- Why stop at learning? [Build your own Git!](https://github.com/codecrafters-io/build-your-own-x#build-your-own-git)
<!-- TODO: Check if required -->

## End