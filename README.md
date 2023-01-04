## git-chsh

<details>
  <summary>srcs:</summary>
  https://www.javatpoint.com/git-cheat-sheet
</details>


## CONFIG

>**git config 3 levels:**  
>	--system //to the whole OS  
>	--global //to the exact user  
>	--project (by default) //to exact project (recorded in config filein proj dir)  
> 🛈 priority | git checking from local level to system  

edit **.git/config** file  
or  
`git config --global <param> <value>`  


<br>

`core.editor.`  
`commit.template`  
`alias`  

`git config --list` show config  


<br><br><br>

## BASIC COMMANDS

`git init` make a new repo  
`git clone <repo path>` clone an existing repo  
`git commit`  
`-m` message  
`-a` add to index(tracked files) and commit  
  
`--amend` rewrite a commit  


 
<br>
 
 
> 🛈 **Best practices** `git commit`  
> \- commit often  
> \- one change - one commit  
> \- commit comment header <= 50 characters  
> \- commit header comment in imperative mood("this commit will fix bugs")  

<br> 
 
 
 
***.git/HEAD***  - Pointer at the current branch. point to the tip of the new branch  
HEAD is you. It points to whatever you checked out, wherever you are. Typically that is not a commit, it is a branch. If HEAD does point to a commit (or tag), even if it's the same commit (or tag) that a branch also points to, you (and HEAD) have been detached from that branch. Since you don't have a branch attached to you, the branch won't follow along with you as you make new commits. HEAD, however, will.  
***Detached HEAD*** - It is possible for HEAD to refer to a specific revision that is not associated with a branch name. This situation is called a detached HEAD.  

reference to commits in code by:  
\- \<id\> - first 4 digit of commit hash  
\- HEAD~4 - 4 previuos commits  
   
 (i): every commit has the link to previuos **parent commit** (or commits in case of merging)  
  
<br> 
 
 
>**3 Zones | (Logical division)**  
> \- Working Directory (local zone)  
> \- Index (intermediate storage of code changes, list of files of working dir tracking by git; repo zone, data in .git)  
> \- Repository HEAD (rep zone, data in .git || history of proj developent)  
  
`git status -s` compact view to see the file state better (untracked - ??, modified - red, staged - green) 
  
  
`git diff` compare files bw working and staged zones
`git diff --staged` compare files bw staged and HEAD zones
`git diff <path>`
  
`git add` add files and changes to staged zone   
`git commit` update HEAD zone w staged files  

 undo commit changes  
`git reset --soft` move only HEAD pointer to \<commit\>  
`git reset` move HEAD and Staged area   
`git reset --hard` move HEAD, staged area, files in working dir
`git reset <path>`  
  
`git checkout HEAD <path>` == `reset --hard`  
`git checkout <path>` update files in working zone frm files from index zone  
`git rm <path>` delete file from working and index zone    
`--chached` safe file  

> **(i) ignoring files**  
> sensetive content passwords  
> big binary files  
> system files from code editors, etc...  
  
create a .gitignore file in the root dir  
  

  
### Check history of commits 
`git log`  
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
  
`git blame <file>` show the authour and commit for every line of the file 
  
`git grep` search in  all files in all commits; use regex 
`-n` show line number
`--count` count of same 


<br>


## REMOTE REPOSITORIES
`git remote -v` список удалённых репозиторие  
`git clone <url репозитория>` загружаем себе копию репозитория, но и неявно отслеживаем удалённый сервер, который находится по указанному адресу и которому присваивается имя origin  
   
`git remote add <имя> <url>` — добавляет удалённый репозиторий с заданным именем;  
`git remote remove <имя>` — удаляет удалённый репозиторий с заданным именем;  
`git remote rename <старое имя> <новое имя>` — переименовывает удалённый репозиторий;  
`git remote set-url <имя> <url>` — присваивает репозиторию с именем новый адрес;  
`git remote show <имя>` — показывает информацию о репозитории.  





`git fetch <имя> <ветка>` — получает данные из ветки заданного репозитория, но не сливает изменения;  
`git pull <имя> <ветка>` — сливает данные из ветки заданного репозитория;  
`git push <имя> <ветка>` — отправляет изменения в ветку заданного репозитория. Если локальная ветка уже отслеживает удалённую, то можно использовать просто git push или git pull.  



**Github Fork**   
GitHub. Это полезно в тех случаях, когда у вас нет прав на создание ветки в оригинальном репозитории. Когда вы воспользуетесь командой git clone, ваш локальный репозиторий будет отслеживать удалённый форк как origin, а оригинальный репозиторий как upstream.  
**Github pull request**   
После этого вам может понадобиться слить тематическую ветку вашего удалённого репозитория в основную ветку оригинального. Для этого вы можете создать новый Pull Request — запрос на внесение изменений, где GitHub проверяет наличие конфликтов прежде чем повзолить вам провести слияние. 


## BRANCHES
`git branch <имя ветки>` 
`git checkout <имя ветки>`  
`-b`  create new branch and switch to it  
`git branch -d <имя ветки>` 
  
`git branch -u <имя удалённого репозитория>/<удалённая ветка>`  
`git checkout --track <имя удалённого репозитория>/<удалённая ветка>`  
`git checkout -b <ветка> <имя удалённого репозитория>/<удалённая ветка>`  

`git branch --vv `  

`git checkout <удалённая ветка>` 



## STASH  


## MERGE  
`git merge <branch2>` 
  
in case of conflicts edit it manully 
```
<<<<<<< HEAD:index.html
Everything above the ==== is the version in master.
=======
Everything below the ==== is the version in the test branch.
>>>>>>> test:index.html
```

## FAST-FORWARD (FF)`
git rebase <основная ветка> <тематическая ветка>`  
  
Перемещайте изменения только на вашей приватной локальной ветке — не перемещайте коммиты, от которых зависит ещё кто-то. 


## rever reset 



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
git rebase -i HEAD~n  
Вы можете поменять порядок коммитов, изменив порядок, в котором они перечислены.  

## message editing / split commit
`edit` Для указания коммита, который вы хотите изменить, используется команда edit  
`git commit --amend` чтобы изменить сообщение или подготовить забытые файлы.  
`git reset HEAD^ ` HEAD будет перемещён на один коммит назад и все изменённые в этом коммите файлы перейдут в статус неподготовленных)  
`git rebase --continue`  

## rewrite some commits 
`git filter-branch`  
`git filter-branch --tree-filter 'git rm -f <имя файла>' HEAD` Например, чтобы удалить случайно зафиксированный файл  
  
/!\учтите, что при этом вся история перемещается.  

## merge commits
pick squash  


## cherry-pick
create a new commit from changes from another branch exact commit  

