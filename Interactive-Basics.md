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

To-do.
