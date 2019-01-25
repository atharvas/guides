[Original Article can be found on the CS225 UIUC Website](https://courses.engr.illinois.edu/cs225/sp2019//guides/git/)
# Getting Started with Git
Welcome CS 225 students to magical world of git, an incredible form of VCS (Version Control System) that we use in CS 225. For those of you not familiar with what VCS is, VCS tend to be used as methods of change-tracking coding projects like your CS 225 assignments. Git is a type of VCS that also utilizes a remote server to keep a secure copy of all your changes both on a remote server and also on your local machine. The tutorial below from [Katacoda Interactive Git Tutorial](https://www.katacoda.com/courses/git) will help you learn the basics of git and walk you through what each command you type is actually doing. Provided further below is a reference for some basic git commands and some information about what each one does.

# Useful Git Reference Sheet
$
```
git init            # Creates/initializes the current folder as a git repository 
git clone <remote>  # Creates a local repository from an already existing remote
                    # repository, where <remote> is the url of the remote repo.

git status          # Prints useful information about the present state of your
                    # local repository relative to the remote repository's state.
git log             # Prints the commit history of the local repository

git add <file>      # Adds the file whose name was passed as a parameter to the 
                    # repository's tracking list, so the repository will now 
                    # keep track of the changes to that file
git rm <file>       # Removes the file whose name was passed as a parameter from
                    # the repository's tracking list as well as removes the file
                    # from your local filesystem. To keep the file locally, 
                    # use the --cached flag.

git checkout        # Used to switch branches or restore working files from the 
                    # remote repo. To restore a specific file, use '-- <file>'
                    # to restore the file where <file> is the name of the file.
git branch <name>   # Used to create a new branch in repo that is named <name>.
git reset           # Reset the current state of the repository to the
                    # specified state. If no state is specified, will default to
                    # the current state of the remote repository. Various options
                    # are available that change the behavior of git reset
git revert          # Used to revert state of current repo to the state of a previous 
                    # commit. Requires local repo to be in the same state as the remote.

git rebase          # Command is used to reduce commits into a compressed change
                    # that can be placed on top of the current state of the remote
                    # repository.

git commit          # Command is used to mark changes that have occured in the repo.

git pull            # Command is used to sync the changes from the remote repository
                    # to the local repository.
git push            # Command is used to sync changes from the local repository to 
                    # the remote repository.

git filter-branch   # This command can be used in case you may have accidentally
                    # pushed your passwords and other secure information into your
                    # repository (please avoid actually doing this). If so, this 
                    # command can help clean your reporitory history to remove
                    # the senstive information. More info at the following link
                    # https://help.github.com/articles/removing-sensitive-data-from-a-repository/

git help            # The most powerful command in git. Use it in your VCS quests.
```
# Some Useful Git Tips:
Our first major tip we want to share with you is to never force push (using ``--force`` with the ``git push`` command). If you are trying to resolve a merge conflict or cannot push due to your branch being behind the remote, using ``git pull`` to first pull the remote changes is the correct approach. Force pushing affects our autograder and may cause your assignments to be ungraded.

One issue we notice students encounter when they need to merge the code in their repository, due to the code in the remote repository having changes that the local repository does not, is that the defualt editor used to edit and save the merge commit message is vim. One thing students tend to do when vim opens, and they don’t know how to quit is choose to force push instead. This is a very bad idea due to the reasons mentioned in the above paragraph. Instead, if you are not comfortable with vim, lets change the default editor used to save the commit message for merges. To do so, please use the command below.

Example For Atom (Can be used on EWS since Atom is on EWS)
$
```
git config --global core.editor "atom --wait"
```
Example For Sublime Text (Cannot be used on EWS since Sublime Text is not on EWS)
$
```
git config --global core.editor "subl -n -w"
```
More information about these git commands and various other git tips and tricks can be found at [Git-SCM](https://git-scm.com/docs).
