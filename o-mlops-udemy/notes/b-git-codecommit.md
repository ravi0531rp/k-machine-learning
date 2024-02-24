## CodeCommit

* Go to Codecommit, and create a new repo.
```sh
git clone https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
```

* Create own repo and add files.
```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/k-machine-learning/o-mlops-udemy/dummy$ cd /home/ravi0531rp
(base) ravi0531rp@ravi-MSI:~$ mkdir my-website
(base) ravi0531rp@ravi-MSI:~$ cd my-website/
(base) ravi0531rp@ravi-MSI:~/my-website$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint: 	git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint: 	git branch -m <name>
Initialized empty Git repository in /home/ravi0531rp/my-website/.git/
(base) ravi0531rp@ravi-MSI:~/my-website$ ls 
appspec.yml  buildspec.yml  CODEDEPLOY.md  code.py  HELP.md  index.html  scripts
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	CODEDEPLOY.md
	HELP.md
	appspec.yml
	buildspec.yml
	code.py
	index.html
	scripts/

nothing added to commit but untracked files present (use "git add" to track)
(base) ravi0531rp@ravi-MSI:~/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   CODEDEPLOY.md
	new file:   HELP.md
	new file:   appspec.yml
	new file:   buildspec.yml
	new file:   code.py
	new file:   index.html
	new file:   scripts/after_install.sh
	new file:   scripts/install_dependencies.sh
	new file:   scripts/start_server.sh
	new file:   scripts/stop_server.sh
	new file:   scripts/validate_service.sh

(base) ravi0531rp@ravi-MSI:~/my-website$ git commit -m "Initial Commit" 
[master (root-commit) 17ff9f5] Initial Commit
 11 files changed, 315 insertions(+)
 create mode 100644 CODEDEPLOY.md
 create mode 100644 HELP.md
 create mode 100644 appspec.yml
 create mode 100644 buildspec.yml
 create mode 100644 code.py
 create mode 100644 index.html
 create mode 100644 scripts/after_install.sh
 create mode 100644 scripts/install_dependencies.sh
 create mode 100644 scripts/start_server.sh
 create mode 100644 scripts/stop_server.sh
 create mode 100644 scripts/validate_service.sh
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/my-website$ git log
commit 17ff9f584ffd3ab791e05d5bcb87f9a09622fb38 (HEAD -> master)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 00:41:06 2024 +0530

    Initial Commit
(base) ravi0531rp@ravi-MSI:~/my-website$ git remote add origin https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo


```
* Go to the IAM user and > Security Credentials > Generate HTTPS git credentials for CodeCommit

```sh
(base) ravi0531rp@ravi-MSI:~/my-website$ git push origin master
Username for 'https://git-codecommit.us-east-1.amazonaws.com': iam_raviroams365-at-992219819011
Password for 'https://iam_raviroams365-at-992219819011@git-codecommit.us-east-1.amazonaws.com': 
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 12 threads
Compressing objects: 100% (11/11), done.
Writing objects: 100% (14/14), 4.33 KiB | 1.08 MiB/s, done.
Total 14 (delta 0), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * [new branch]      master -> master

```

* More on staging area and other commands
```sh
git diff ---> gives diff between working directory and staged version
git diff --staged ---> diff between staged version and committed version
git status -v -v ---> detailed status
```

```sh
(base) ravi0531rp@ravi-MSI:~/my-website$ touch hello.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ touch cat.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ echo "hello" > hello.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ echo "Meow" > cat.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ ls
appspec.yml  buildspec.yml  cat.txt  CODEDEPLOY.md  code.py  hello.txt  HELP.md  index.html  scripts
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	cat.txt
	hello.txt

nothing added to commit but untracked files present (use "git add" to track)
(base) ravi0531rp@ravi-MSI:~/my-website$ git add *.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   cat.txt
	new file:   hello.txt

(base) ravi0531rp@ravi-MSI:~/my-website$ git diff --staged
diff --git a/cat.txt b/cat.txt
new file mode 100644
index 0000000..92777d5
--- /dev/null
+++ b/cat.txt
@@ -0,0 +1 @@
+Meow
diff --git a/hello.txt b/hello.txt
new file mode 100644
index 0000000..ce01362
--- /dev/null
+++ b/hello.txt
@@ -0,0 +1 @@
+hello

```

* Unstaging from 1) Local Repo to Staging Area 2) Staging area to Working Directory

```sh
(base) ravi0531rp@ravi-MSI:~/my-website$ touch unstage.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ echo "Unstaged" > unstage.txt 
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   cat.txt
	new file:   hello.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	unstage.txt

(base) ravi0531rp@ravi-MSI:~/my-website$ git add unstage.txt 
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   cat.txt
	new file:   hello.txt
	new file:   unstage.txt

(base) ravi0531rp@ravi-MSI:~/my-website$ git commit -m "New file unstage.txt added"
[master f6ec357] New file unstage.txt added
 3 files changed, 3 insertions(+)
 create mode 100644 cat.txt
 create mode 100644 hello.txt
 create mode 100644 unstage.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ git log
commit f6ec357b92618239be005358c54243f335e73f7c (HEAD -> master)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 02:46:29 2024 +0530

    New file unstage.txt added

commit 17ff9f584ffd3ab791e05d5bcb87f9a09622fb38 (origin/master)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 00:41:06 2024 +0530

    Initial Commit
(base) ravi0531rp@ravi-MSI:~/my-website$ echo "New changes" > unstage.txt 
(base) ravi0531rp@ravi-MSI:~/my-website$ git diff
diff --git a/unstage.txt b/unstage.txt
index 5133535..d3767ac 100644
--- a/unstage.txt
+++ b/unstage.txt
@@ -1 +1 @@
-Unstaged
+New changes
(base) ravi0531rp@ravi-MSI:~/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/my-website$ git diff
(base) ravi0531rp@ravi-MSI:~/my-website$ git diff --staged
diff --git a/unstage.txt b/unstage.txt
index 5133535..d3767ac 100644
--- a/unstage.txt
+++ b/unstage.txt
@@ -1 +1 @@
-Unstaged
+New changes
(base) ravi0531rp@ravi-MSI:~/my-website$ git reset HEAD unstage.txt
Unstaged changes after reset:
M	unstage.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   unstage.txt

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/my-website$ git reset --soft HEAD^
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   cat.txt
	new file:   hello.txt
	new file:   unstage.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   unstage.txt

(base) ravi0531rp@ravi-MSI:~/my-website$ git log
commit 17ff9f584ffd3ab791e05d5bcb87f9a09622fb38 (HEAD -> master, origin/master)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 00:41:06 2024 +0530

    Initial Commit

(base) ravi0531rp@ravi-MSI:~/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/my-website$ git commit -m "Second Commit"
[master 4a05a2e] Second Commit
 3 files changed, 3 insertions(+)
 create mode 100644 cat.txt
 create mode 100644 hello.txt
 create mode 100644 unstage.txt
(base) ravi0531rp@ravi-MSI:~/my-website$ git status
On branch master
nothing to commit, working tree clean


```

* Hard Reset and Revert
```sh
git reset --hard HEAD^
git reset --hard HEAD^^

git revert <commit_id> # generates new commit


```

* AWS Codecommit Remote Git Commands

```sh
git remote add origin <url>

git remote -v # display remote repos

git remote add dev2 <url> # add a new remote

git remote rm <name>

git push -u <remote> <branch>

```

* AWS Codecommit Clone and Branching

```sh
git clone <repo link>

git pull origin master

```

* Branching and Changes ; Maintain Branches and Merge when necessary

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ls
appspec.yml  buildspec.yml  CODEDEPLOY.md  code.py  HELP.md  index.html  scripts
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch master
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout -b dev
Switched to a new branch 'dev'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch dev
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch dev
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Rename Title"
[dev 78c3c20] Rename Title
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch
* dev
  master
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push origin dev
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 295 bytes | 295.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * [new branch]      dev -> dev
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git log
commit 78c3c20e34f69274955c87ca29d0c2b926d72d89 (HEAD -> dev, origin/dev)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Thu Feb 1 23:21:43 2024 +0530

    Rename Title

commit 45c5c77bca24aeec7c9cbd858a002c261b2390ed (origin/master, master)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Thu Feb 1 16:18:34 2024 +0530

    Remove unnecessary files

commit 4a05a2e3045a594150090b53548861e235ea76db
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 02:57:19 2024 +0530

    Second Commit

commit 17ff9f584ffd3ab791e05d5bcb87f9a09622fb38
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 00:41:06 2024 +0530

    Initial Commit


```

Now raise PR and get it merged! And now delete the current branch.
```sh
git branch -d dev
git push -d origin dev # delete from remote
git branch -D dev # to remove an unmerged branch
```

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch -d dev
error: The branch 'dev' is not fully merged.
If you are sure you want to delete it, run 'git branch -D dev'.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git pull 
From https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
   45c5c77..78c3c20  master     -> origin/master
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream-to=origin/<branch> master

(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git pull origin master
From https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * branch            master     -> FETCH_HEAD
Updating 45c5c77..78c3c20
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch -d dev
Deleted branch dev (was 78c3c20).
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push -d origin dev
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 - [deleted]         dev


```

* Handling Conflicts

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch team1
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout -b team2
Switched to a new branch 'team2'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout -b team1
fatal: A branch named 'team1' already exists.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout team1
Switched to branch 'team1'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch team1
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch team1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Team 1 Made Changes"
[team1 adc62bd] Team 1 Made Changes
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push origin team1
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 318 bytes | 318.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * [new branch]      team1 -> team1

```
Now go ahead and create PR on AWS. And merge this to master. And pull locally in master.
And make some changes in same line in team2 branch to create conflict.
Once you try to merge team2 code to master, vscode will automatically open conflict
resolution mode.

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git pull origin master
From https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * branch            master     -> FETCH_HEAD
   78c3c20..adc62bd  master     -> origin/master
Updating 78c3c20..adc62bd
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout team2
Switched to branch 'team2'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch team2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Note we made changes here. Thats why it says modified
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Team 2 Changes"
[team2 f810484] Team 2 Changes
 1 file changed, 3 insertions(+), 3 deletions(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Let's take a shortcut to better see merge conflict
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git merge team2
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.


```

* Resolve in VSCODe using pick and choose. And then complete the merge.

```sh

base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git log
commit f7b1947ee4bb7dd1e997f8f4d2fb44efc91308c5 (HEAD -> master)
Merge: adc62bd f810484
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Fri Feb 2 00:22:34 2024 +0530

    Merge branch 'team2'

commit f810484e9857ff5f4d2b6987866a494d941a558f (team2)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Fri Feb 2 00:13:29 2024 +0530

    Team 2 Changes

commit adc62bd6ab5006eb874bf6554b47e5e430a0dbae (origin/team1, origin/master, team1)
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Fri Feb 2 00:03:36 2024 +0530

    Team 1 Made Changes

commit 78c3c20e34f69274955c87ca29d0c2b926d72d89
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Thu Feb 1 23:21:43 2024 +0530

    Rename Title

commit 45c5c77bca24aeec7c9cbd858a002c261b2390ed
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Thu Feb 1 16:18:34 2024 +0530

    Remove unnecessary files

commit 4a05a2e3045a594150090b53548861e235ea76db
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 02:57:19 2024 +0530

    Second Commit

commit 17ff9f584ffd3ab791e05d5bcb87f9a09622fb38
Author: ravi0531rp <ravi.0531.rp@gmail.com>
Date:   Wed Jan 31 00:41:06 2024 +0530

    Initial Commit

(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push origin master
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Delta compression using up to 12 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 632 bytes | 632.00 KiB/s, done.
Total 6 (delta 4), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
   adc62bd..f7b1947  master -> master

```

* Git Merge vs Git Rebase
Whatever branch we are working, what if we have made some changes but other branch got merged.
Now, We made some more changes, but we need to pull in the changes as well. And continue working.
What to do??

```sh

(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch -d team1
Deleted branch team1 (was adc62bd).
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git branch -d team2
Deleted branch team2 (was f810484).
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push -d origin team1
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 - [deleted]         team1
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git log --oneline
f7b1947 (HEAD -> master, origin/master) Merge branch 'team2'
f810484 Team 2 Changes
adc62bd Team 1 Made Changes
78c3c20 Rename Title
45c5c77 Remove unnecessary files
4a05a2e Second Commit
17ff9f5 Initial Commit
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout -b feature/temp
Switched to a new branch 'feature/temp'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## make changes
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Changes to feature branch"
[feature/temp 7ec3c28] Changes to feature branch
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git merge feature/temp
Updating f7b1947..7ec3c28
Fast-forward
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## This was fast forward merge. Happy happy. No problems at all..
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Again checkout to feature branch, and make changes for testing.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout feature/temp
Switched to branch 'feature/temp'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "feature/temp commit"
[feature/temp 379d117] feature/temp commit
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Make some more changes
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "More changes in feature/temp"
[feature/temp 512ab6a] More changes in feature/temp
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Do some changes in master to emulate changes maerged from a different branch
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "New Changes to the master branch"
[master 0aa96f5] New Changes to the master branch
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Do more changes and commit
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "More changes to master"
[master 1241d86] More changes to master
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## master branch is two commits ahead of feature branch
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## see what happens when we try to merge
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Even if we resolve it, it adds a new commit on top of it. That's not the right thing to do.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Since we are still working, we need to get the updated code from master in our feature branch. But without adding a commit
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## It gets messy
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Hence Rebase
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout feature/temp
index.html: needs merge
error: you need to resolve your current index first
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
	both modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add .
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Master changes"
[master 69ac158] Master changes
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout feature/temp
Switched to branch 'feature/temp'

(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git rebase master
Successfully rebased and updated refs/heads/feature/temp.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git rebase master
error: cannot rebase: You have unstaged changes.
error: Please commit or stash them.

tensorflow-env) (torch-env) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Changes taken from master"
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Changes taken from master"
[feature/temp 9683a62] Changes taken from master
 1 file changed, 4 deletions(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git rebase master
Current branch feature/temp is up to date.
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git log --oneline
9683a62 (HEAD -> feature/temp) Changes taken from master
69ac158 (master) Master changes
1241d86 More changes to master
0aa96f5 New Changes to the master branch
512ab6a More changes in feature/temp
379d117 feature/temp commit
7ec3c28 Changes to feature branch
f7b1947 (origin/master) Merge branch 'team2'
f810484 Team 2 Changes
adc62bd Team 1 Made Changes
78c3c20 Rename Title
45c5c77 Remove unnecessary files
4a05a2e Second Commit
:...skipping...
9683a62 (HEAD -> feature/temp) Changes taken from master
69ac158 (master) Master changes
1241d86 More changes to master
0aa96f5 New Changes to the master branch
512ab6a More changes in feature/temp
379d117 feature/temp commit
7ec3c28 Changes to feature branch
f7b1947 (origin/master) Merge branch 'team2'
f810484 Team 2 Changes
adc62bd Team 1 Made Changes
78c3c20 Rename Title
45c5c77 Remove unnecessary files
4a05a2e Second Commit
17ff9f5 Initial Commit

```

Also, if the changes were in the remote master branch(which is normally the case),
then just go to the feature bfranch and type 
```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch master
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push origin master
Enumerating objects: 20, done.
Counting objects: 100% (20/20), done.
Delta compression using up to 12 threads
Compressing objects: 100% (18/18), done.
Writing objects: 100% (18/18), 1.78 KiB | 1.78 MiB/s, done.
Total 18 (delta 13), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
   f7b1947..69ac158  master -> master
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout feature/temp
Switched to branch 'feature/temp'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git pull --rebase origin master
From https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
 * branch            master     -> FETCH_HEAD
Current branch feature/temp is up to date.

```
Also, never rebase once you have pushed to remote on your feature branch.

* Git Stash
What if there's a scenario in which we are having to checkout to other branch, while there
are uncommitted changes. Either commit or Stash. But we dont wanna commit unnecessarily.

```sh
git stash save "message"
git stash list
git stash apply <stashid> 
git stash pop # Apply the top changes to my file
git stash drop <stashid> # drop 
git stash clear # drop all stashes

```

Now lets work on this.

```sh
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
error: Your local changes to the following files would be overwritten by checkout:
	index.html
Please commit your changes or stash them before you switch branches.
Aborting
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash save "stash demo"
Saved working directory and index state On temp: stash demo
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout master
Switched to branch 'master'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ ## Do whatever you wanted to...
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git add index.html 
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git commit -m "Faltu commit on master"
[master db68621] Faltu commit on master
 1 file changed, 1 insertion(+), 1 deletion(-)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git push origin master
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 12 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 302 bytes | 302.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Validating objects: 100%
To https://git-codecommit.us-east-1.amazonaws.com/v1/repos/codecommit-demo
   69ac158..db68621  master -> master
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout feature/temp
Switched to branch 'feature/temp'
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash list
stash@{0}: On temp: stash demo
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash apply 0
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash list
stash@{0}: On temp: stash demo
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git checkout -- .
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git status
On branch feature/temp
nothing to commit, working tree clean
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash list
stash@{0}: On temp: stash demo
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash pop
On branch feature/temp
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (c4143ce0713678e21c584793231e12cc68e4f6c2)
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ git stash list
(base) ravi0531rp@ravi-MSI:~/Desktop/CODES/u-miscellaneous/my-website$ 



```

* Codecommit Security
We have condition policy from IAM. and assign explicit deny to the user group in which Junior is present so that they cant merge. And in the policy json, we mention the ARN of the repo.
Also, can mention the branch names to which this deny applies.

* Notification
Well, we can set up notifications
Go to repo > notify > create notification rule > ..
We can set when to trigger. 
and the target. 1) SNS topic 2) AWS CHATBOT

* Triggers
Go to settings of repo > Triggers > Create Trigger > 
Select Event as well as branches
Where to send notifications..

* Cloudwatch
This is the most important. We can set Rules and then a certain change in repo can be tagged
to a target like a lambda function, Codebuild..
And we can have service partners as well, it doesn't have to be within the ecosystem.