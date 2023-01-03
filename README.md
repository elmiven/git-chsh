## git-chsh

#### Config

edit .gitconfig 
or
git config --global <param> <value>

core.editor.
commit.template
alias 
 
git config --list


#### Basic commands

git init //make a new repo
git clone <repo path> //clone an existing repo 

it commit
-m \\message 
-a \\add to index(tracked files) and commit

--amend \\rewrite a commit 

>**Best practices:** 
>commit often
>one change - one commit 
>make commit header <= 50 characters. Imperative mood("this commit will fix bugs")

.git/HEAD - pointer at the current branch. point to the tip of the new branch
Detached HEAD - It is possible for HEAD to refer to a specific revision that is not associated with a branch name. This situation is called a detached HEAD.
HEAD is you. It points to whatever you checked out, wherever you are. Typically that is not a commit, it is a branch. If HEAD does point to a commit (or tag), even if it's the same commit (or tag) that a branch also points to, you (and HEAD) have been detached from that branch. Since you don't have a branch attached to you, the branch won't follow along with you as you make new commits. HEAD, however, will.


