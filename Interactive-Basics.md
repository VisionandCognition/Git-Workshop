Setup
=====

Create user on Github
---------------------

https://github.com/join

Generate and add SSH key
----------------

### Generate the SSH Key

https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

### Add Key

https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/

Install git
-----------

For Debian/Ubuntu: `sudo apt-get install git`

For Windows, I (Jonathan) personally like TortoiseGit: https://tortoisegit.org/download/

Macs?

Create New Repository
=====================

Create Local Repository
-----------------------

Create a new directory, such as "git-demo". Open the directory in a command console / terminal or `Git Bash`. Type the following:

    git init

This will create a ".git" subdirectory that will store the repository, which contains all the versions of all the files and the commits etc. You can peak inside by typing `ls .git`.

Create a file, for example "helloworld.m" with the following:

    fprintf("Hello world!")
    
It's okay that there are errors (we will change it later).

Type `git status`. It will list `helloworld.m` as being untracked. This means that it is not yet part of the repository and changes will not be kept.

Now add the file and show that status again:

    git add helloworld.m
    git status
    
The file is now "staged" to be added in the next commit. It still has not yet been added to the repository. The file needs to be committed for it to be added to the repository and tracked.

    git commit -m "Add helloworld.m."
    
Now if you do `git status`, you will see that everything is up-to-date.

Let's delete the file by "accident" or make changes that you want to remove. To recover the current version, type `git checkout helloworld.m`.

Git checkout can also "checkout" different versions or branches of a repository.

Create Remote Repository
------------------------

Create a new repository on Github, without any README file, .gitignore, etc. Name it `git-demo` for this workshop.

Full instructions can be found here:
https://help.github.com/articles/creating-a-new-repository/

When done, follow the "Quick setup" step, ie. copy the URL for the repository. It should be something like this: "git@github.com:your_username/git-demo.git".

Go back into the console and use that URL to connect your local repository to Github:

    git remote add origin YOUR_URL

Then type `git remote -v` to view the connection and then push your current commit to remote.

    git push origin master

`origin` is where you are pushing. `master` is the branch that you are pushing.

You can refresh your browser (with your github repository) to see the current files.

Do the following using the browser (a **BAD** idea for code in real scenarios):

* Create a README file.
* Modify the file that you created.

Move the helloworld file
------------------------

Make a directory named "code" and move the helloworld.m file to it. There is a simple way and slightly more complicated way to move or rename files that are in Git. The simple way is to use the command `git mv`. The more complicated way is to use `mv` and then add the file in the new location to git (`git add`) and also stage the "delete" of the file in the old location (also `git add`). If you do `git status` it should say that git has detected a renaming of "helloworld.m".

Get changes from made on Github
-------------------------------

Type:

    git fetch
    git rebase

it will probably give an error, read it. I would recommend doing the following to fix it:

    git remote -v
    git branch --set-upstream-to=origin/master master

Checkout the state of the files in your directory. Does helloworld have all the changes?

Additional changes
------------------

Change the helloworld.m script if there is enough time. Use `git diff` to see unstaged changes.

Encounter and solve a merge conflict
====================================

Fork Jonathan's repository to be able to edit it (go to https://github.com/williford/git-demo and click fork). It will automatically switch to your fork. 

Now move to your git bash command line, cd into your favorite location, and type `git clone git@github.com:username/git-demo.git`. 

If you were to open the helloworld.m file in matlab, edit it, commit it, and push it back to your fork, we would not encounter a merge conflict, because the files on the fork haven't changed. However, we are going to simulate a situation in which other people also work on this file. 

Let's go ahead and make the 'other people changes' first. In the browser, look for helloworld.m and click the little pencil to edit the code. 

Add something to the code on line 3. For example, append it with `fprintf('a good day to you my friend');`, or simply change the exclamation point into a question mark. Go ahead and commit this change, and pretend it was someone else who did it :) 

Switch back to editing locally and open helloworld.m in matlab. This should still contain the old line 3: 

`fprintf('Hello world!');` 

because we are pretending that someone else is changing the remote code at the same time as we are changing our local copy. So now change line 3 in your local copy, but change it into something new (if you make the exact change that you made on the server, it will not lead to a merge conflict). 

Next, commit this change as usual, you should not run into trouble. However, if now you try to push, git tells you no because the cannot merge. This is called a merge conflict and it occurs because git doesn't know which of the two changes it should pick. So let's solve it. 

Solving the merge conflict 
--------------------------

Start by fetching the changes that the 'other' people secretly made while you were gone, `git fetch`. 

After fetching, type `git merge`. This won't work, but it will bring git into a state of conflict. If you use the git bash on windows, the directory indicator will say `(master|MERGING)` at the end of the line, instead of `(master)`.

We will solve this conflict in Matlab. If you refresh the current folder, you will see a little red exclamation point warning next to the helloworld.m file in the Git column to indicate that there is a conflict going on. In the file itself you will see a bunch of weird comments that show both verions of all the conflicting lines (in this case, only line 3). Git uses these comments to tell matlab where the conflict is. 

Right click the file helloworld.m and click 'extract conflict markers to file'. Leave the settings as they are and click 'extract'. This will remove those weird comments and open a window for you to solve the conflict. 

In this window, you will see the remote file that you just fetched on the left, and your own file on the right. Conflicts are marked in red. If you highlight a conflict, the 'merge' button becomes clickable. When you click merge, the remote line is copied over your own line. If you don't click merge, you keep your own line. 

After you're done deciding which lines to merge and which lines not to, just close the window. You have now resolved the conflict by picking which versions of which lines you want to keep. Right click the helloworld.m file again and select 'Mark Conflict Resolved'. Now you can delete the 'helloworld_theirs.m' file that matlab created to aid the resolution. 

You are now ready to commit your work and push it to the server. Your conflict has been solved. 




