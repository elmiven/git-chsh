## [git cheat sheet]


  <summary>srcs:</summary>
  https://training.github.com/ - github cheat sheet<br>
  https://ndpsoftware.com/git-cheatsheet.html - interactive cheat sheet<br>
  https://www.atlassian.com/git/tutorials/atlassian-git-cheatsheet - git cheat sheet<br>
  https://www.javatpoint.com/git-cheat-sheet - git cheat sheet<br>
  https://git-scm.com/docs/giteveryday - tut basic commands<br>
 
  https://system-admins.ru/komandy-git-shpargalka-dlya-sysadmin-i-devops/ - cheat sheet (ru)
  https://marklodato.github.io/visual-git-guide/index-ru.html - cheat sheet (ru)
    
  https://githowto.com - interactive tut  
  https://gitimmersion.com/ - interactive tut  
  https://git-scm.com/docs/gittutorial - tut
  https://git-scm.com/doc - docs and book 
    
  
  https://www.sourcetreeapp.com - git GUI app 
  
</details>

<br><br>

> **3 main zones of git | (Logical division)**  
> \-  (stash)  
> **\- Working Directory** (local zone)  
> **\- Index/staged** (intermediate storage of code changes, list of files of working dir tracking by git; repo zone, data in .git)  
> **\- Local repository** HEAD (rep zone, data in .git || history of proj developent)  
> \-   (Upsteam/remote repository)


<br><br>    
  
## CONFIG
 
>**git config 3 levels:**  
>	--system //to the whole OS  
>	--global //to the exact user  
>	--project (by default) //to exact project (recorded in config filein proj dir)  
> *🛈 priority | git checking from local level to system*

<br>

> **git config settings:**  
> -\> edit **.git/config**   
>-\> `git config --global <param> <value>`  

<br>

**Name and Email**  
`git config --global user.name "Your Name"`  
`git config --global user.email "your_email@whatever.com"`  
  
**Line Ending Preferences**    
for Unix/Mac users:  
`git config --global core.autocrlf input`  
`git config --global core.safecrlf true`  
for Windows users:`  
`git config --global core.autocrlf true`  
`git config --global core.safecrlf true`   


**Display UTF-8 characters in filenames** if you're having problems seeing them  
`git config --global core.quotepath false`  
  
**change the default commit comment editor**  
`core.editor.`   
  
**template for commit comments**  
`commit.template`   

<br>

**aliases**  
`git config --global alias.co checkout`  
  
.git/config  
```
[alias]
  co = checkout
  ci = commit
  st = status
  br = branch
  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
  type = cat-file -t
  dump = cat-file -p
```  
Command aliases (you can add aliases on this level If your shell supports it) 
```
alias gs='git status '
alias ga='git add '
alias gb='git branch '
alias gc='git commit'
alias gd='git diff'
alias gco='git checkout '
alias gk='gitk --all&'
alias gx='gitx --all'
alias got='git '
alias get='git '
```
<br>

**show config  settings**
`git config --list` 




<br><br><br>

## BASIC COMMANDS
>**to start new proj:**  
>`git init` make a new repo  
>`git clone {repo path}` clone an existing repo , a local version of a repository, including all commits and branches  

<br>

**status**  
`git status -s` check status of git zones.  
`-s` compact view to see the file state better (untracked - ??, modified - red, staged - green)  

<br>

**add** (add files to staged/index zone & start tracking their changes)  
`git add` add files and changes to staged zone  
`git add . ` add files of current dir  
`git add -A` add files of all die  

<br>

**commit**  (Git object, a snapshot of your entire repository compressed into a SHA)  
`git commit` update HEAD zone w staged files  
`-m` message  
`-a` add to inx(tracked files) and commit  
`--amend` rewrite a commit  

<br>  
> 🛈 **Best practices** `git commit`  
> \- commit often  
> \- one change - one commit  
> \- commit comment header <= 50 characters  
> \- commit header comment in imperative mood("this commit will fix bugs")  

<br> 
**.git/HEAD:** pointer, representing your current working directory(eg point to the tip of the new branch), the HEAD pointer can be moved to different branches, tags, or commits when using `git checkout`  
"HEAD is you. It points to whatever you checked out, wherever you are. Typically that is not a commit, it is a branch. If HEAD does point to a commit (or tag), even if it's the same commit (or tag) that a branch also points to, you (and HEAD) have been detached from that branch. Since you don't have a branch attached to you, the branch won't follow along with you as you make new commits. HEAD, however, will."  
***Detached HEAD***: It is possible for HEAD to refer to a specific revision that is not associated with a branch name. This situation is called a detached HEAD.  

🛈: Reference to commits in code:  
\-\> \<id\> - first 4 digit of commit hash  
\-\> HEAD~4 - 4 previuos commits  

🛈: every commit has the link to previuos **parent commit** (or many commits in case of merging)  

<br>  


**.gitignore** ignore unwanted files  
create a `.gitignore` file in the root dir  
> sensetive content passwords  
> big binary files  
> system files from code editors, etc...  
    
<br>


**Diff (Compare files in git zones)  
`git diff` compare files bw working and staged zones  
`git diff --staged` compare files bw staged and HEAD zones  
`git diff <path>`  
  
<br>

### Check history of commits 
**log**  
`git log` show the history of all commmits    
`-p`  
`--stat`  
`-n`  
`--since="yyy-mm-dd" --until="yyy-mm-dd"`  
`--pretty=oneline`  
`--pretty=format`  
`grep -s`  
`--no-merges`  
`branch1..branch2`  
`branch1...branch2`  
`-L`  
`--all` flag makes sure that we see all the branches **(w tags!)**. The default is to show only the current branch.  

**blame**  
`git blame <file>` show the authour and commit for every line of the file.

**grep**  
`git grep` search in  all files in all commits; use regex  
`-n` show line number  
`--count` count of same     
  
> 🛈: use tags    


<br>

 ### Undo commit changes  
**checkout {path}**   
`git checkout <path>` Discarding local changes (before staging)    

**reset**    
`git reset --soft` move only HEAD pointer to \<commit\>  
`git reset` move HEAD, reset Staged area   
`git reset --hard` move HEAD, reset staged area, reset files in working dir
`git reset <path>`  

**checkout HEAD {path}**  
`git checkout HEAD <path>` == `reset --hard`  

**rm**  
`git rm <path>` delete file from working and index zone    
`--chached` delete file only fromm index zone    

**revert**  
`git revert` To undo a committed change, generate a commit that removes the changes introduced by our unwanted commit.      

**mv**  
`git mv {file} {dir}` move file  

**commit --amend**  
`git commit --amend` change/amend exisitng last commit 

<br>

> Removed commit are still in the system just in detached state from the brach, we can reach it by hash or bt tag if we taged it.  
> Commits that are unreferenced remain in the repository until the system runs the garbage collection software. 
> /!\: reset are safe for local rep, but if  branch is shared on remote repositories, resetting can confuse other users sharing the branch!  


<br>

### tagging 

`git tag v1 `  Now you can refer to the current version of the program as v1. 
git checkout v1^  go to the previous commit  
`git checkout v1~1` the same  go to the previous commit in different   
`@{-1}`  the same as HEAD~1  
`git tag -d oops` delete tag  
`git tag` show tags  


<br><br>

## BRANCHING

**branch**  
`git branch <branch name>` create a branch  
`git branch -d <branch name>` delete branch   
`git branch` show branches  
` --vv` detailed info about branches

**checkout {branch}**  
`git checkout <branch name/HEAD/id` switch to the branch   
`-b`  create new branch and switch to it  




<br>

### merge (conflicts) / rebase(fast-forward ff)  
**merge**  
`git merge <branch2>` merge current branch(usualy master branch) with pointed one  

**merge (Conflicts!)**
in case of conflicts edit it manully:  
```
<<<<<<< HEAD:index.html
Everything above the ==== is the version in master.
=======
Everything below the ==== is the version in the test branch.
>>>>>>> test:index.html
```
/!\\: commit after fix the conflict!  


**rebase** (fast-forward(ff))    
`git rebase <main-branch> <new-branch>`  



>**Merge VS Rebase**
>The final result of the rebase is very similar to the merge. The greet branch now contains all of its changes, as well as all the changes from the master >branch. However, the commit tree is quite different. The commit tree for the greet branch has been rewritten so that the master branch is a part of the >commit history. This leaves the chain of commits linear and much easier to read.  
>**When to Rebase, When to Merge?**
>Don’t use rebase …
>    If the branch is public and shared with others. Rewriting publicly shared branches will tend to screw up other members of the team.
>    When the exact history of the commit branch is important (since rebase rewrites the commit history).>
>
>Given the above guidelines, I tend to use rebase for short-lived, local branches and merge for branches in the public repository.  

<br> 




### stash  


<br><br>

  
  
  
## REMOTE REPOSITORIES

**clone**  
`git clone <repo url>` download a copy of the repo, and  implicitly tracked remote server nammed "origin"  
 
**remote**  
 `git remote -v` list of remote repos     
  
`git remote add <name> <url>` — добавляет удалённый репозиторий с заданным именем;  
`git remote remove <name>` — удаляет удалённый репозиторий с заданным именем;  
`git remote rename <old name> <new name>` — переименовывает удалённый репозиторий;  
`git remote set-url <name> <url>` — присваивает репозиторию с именем новый адрес;  
`git remote show <name>` — показывает информацию о репозитории.  

>Remote repositories typically live on a separate machine, possibly a centralized server. As we can see here, however, they can just as well point to a repository on the same machine. There is nothing particularly special about the name “origin”, however the convention is to use the name “origin” for the primary centralized repository (if there is one).
>  

**branch -a | --track**  
`git branch -a` show inf abt remote branches  
`git branch --track feature origin/feature` Add a local branch that tracks a remote branch.  
`git branch -a`
  

`git branch -u <remote-repo-name>/<remote-branch>` change the upstream info  

  
`git checkout -b <ветка> <remote-repo-name>/<remote-branch>`  
`git checkout <remote-branch>` 


<br>

**--bare**  
`git clone --bare name namrdir.git` create a bare repo (repo without a workspace(working zone))  

> **bare repository** will serve as the origin repository for several remote users, so it does not create the default remote origin. What this means is that basic git pull and git push operations won't work since Git assumes that without a workspace, you don't intend to commit any changes to the bare repository:
  
`git remote add shared ../hello.git` Adding a Remote Repository  
`git push shared master`  
>Since bare repositories are usually shared on some sort of network server, it is usually difficult to cd into the repo and pull changes. So we need to push our changes into other repositories.
shared is the name of the repository receiving the changes we are pushing. (Remember, we added it as a remote in the previous lab.)


**fetch / merge**  
`git fetch <name> <branch>` — fetch new commits from the remote repository, but it will not merge these commits into the local branches.  
`git merge origin/master` - Merge the fetched changes into local master

Add a local branch that tracks a remote branch.  

**pull**  
`git pull <name> <branch>` — fetch and merge  
**push**  
`git push <name> <branch>` — отправляет изменения в ветку заданного репозитория. Если локальная ветка уже отслеживает удалённую, то можно использовать просто git push или git pull.  

`git remote add shared ../hello.git`  
`git branch --track shared master`  
`git pull shared master`  
  


**Github Fork**   
GitHub. Это полезно в тех случаях, когда у вас нет прав на создание ветки в оригинальном репозитории. Когда вы воспользуетесь командой git clone, ваш локальный репозиторий будет отслеживать удалённый форк как origin, а оригинальный репозиторий как upstream.  
**Github pull request**   
После этого вам может понадобиться слить тематическую ветку вашего удалённого репозитория в основную ветку оригинального. Для этого вы можете создать новый Pull Request — запрос на внесение изменений, где GitHub проверяет наличие конфликтов прежде чем повзолить вам провести слияние. 






<br><br>


## ADVANCED USAGE 


### interactive console for staged zone 

`git add -i`  
`status`  
`update`  
`revert`  
`add untracked`  
`patch`  
`diff`   
`quit`  
`help`  
*  

## history editing
`git rebase -i HEAD~n`    
Вы можете поменять порядок коммитов, изменив порядок, в котором они перечислены.  

## message editing / split commit
`edit` Для указания коммита, который вы хотите изменить, используется команда edit  
`git commit --amend` чтобы изменить сообщение или подготовить забытые файлы.  
`git reset HEAD^ ` HEAD будет перемещён на один коммит назад и все изменённые в этом коммите файлы перейдут в статус неподготовленных)  
`git rebase --continue`  

## rewrite some commits 
`git filter-branch`  
`git filter-branch --tree-filter 'git rm -f <имя файла>' HEAD` Например, чтобы удалить случайно зафиксированный файл  
  
/!\ учтите, что при этом вся история перемещается.  

## merge commits
pick squash  


## cherry-pick
create a new commit from changes from another branch exact commit  


## Start up the git server  
Execute From the work directory:  
`git daemon --verbose --export-all --base-path=.`  
Now, in a separate terminal window, go to your work directory
Execute From the work directory:  
```
git clone git://localhost/hello.git network_hello  
cd network_hello  
ls  
```
You should see a copy of hello project.
Pushing to the Git Daemon

If you want to push to the git daemon repository, add --enable=receive-pack to the git daemon command. Be careful because there is no authentication on this server, anyone could push to your repository.


    Learn to share repos across WIFI.

See if your neighbor is running the git daemon. Exchange IP addresses and see if you can pull from each other’s repositories.

NOTE: The gitjour gem is really useful in sharing ad-hoc repositories.



---
.git/refs  
.git/refs/heads  
.git/refs/tags  
  
