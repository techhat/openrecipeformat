Introduction to Git
===================

Using a text-based format, especially YAML, provides a powerful platform for
recipe management. Recipes are essentially source code, using a human compiler
rather than a machine compiler. As such, they can benefit from many of the same
tools as computer programming languages. One of these tools that can be
especially powerful in kitchen lab environments and recipe development is
version control. Unfortunately, most cooks are not used to using version
control, especially git.

This document is currently targeted at developers and other technical
professionals who are more used to using command line-based software. It assumes
that the user has not previously used git, but can follow along with command
line instructions. It was written for the Linux environment, but other Unices
should not differ too terribly. Another guide, targeted at graphical
environments such as Gnome, KDE and Windows, is planned.


Distributed Revision Control
============================
Classical revision control systems used a centralized repository server, from
which a user could check out files, modify them, and check them back in. Some
older systems, such as CVS, would maintain version numbers of the repository
as a whole; even checking in changes to a single file would update the version
of every file in the repository. Some newer systems such as Subversion would
maintain individual version numbers on each file. In either case, the central
repository server would manage the version numbers, and was the final word on
conflicting versions of files that were checked in.

This scenerio was common in the software industry, and tended to work well for
small software projects. However, it posed several limitations in larger
organizations, which needed to handle multiple, disparate branches of a project
in multiple, disparate locations. A distributed solution was needed. Several of
these now exist, each with their own strengths. This guide focuses on git,
partly because of its current popularity, and partly because of the author's
own persional experience.

Git was written by Linus Torvalds, creator of the Linux operating system kernel.
It does not inherently assume a central repository, which controls all other
checkouts of a project. Each user maintains their own repository, and with it
the ability to send patches to another copy of the repository, and merge
patches sent from another copy of the repository.

When a repository is copied from another source, it is known as a fork. The
process of forking a repository in git uses the `clone` command. Forked
repositories can `pull` changes from other forks, or from the repository that
they were cloned from. Forks can also send changes upstream to the initial
repository using, among other options, a "pull request", in which the initial
repository pulls changes from a fork.

Confused yet? Don't worry, we'll take it step by step.


Initializing a Repo
===================
This guide assumes the use of GitHub, a popular site which maintains Git
repositories (known as "repos"), using both free and paid models. There are
other stellar hosting options available, but by and large the usage will be the
same.

If you haven't already, go to https://github.com/ and create an account. Once
you have signed up, you need to create a new repo. In GitHub, the icon to create
a new repo is located in the top-right corner of the page, and looks like a book
with a plus sign on it. Call your repo "myrecipes", and go ahead and make it
public.

Once the repo has been created on GitHub, you need to initialize it on your
local machine. 

.. code-block:: bash

    localhost> mkdir -p ~/git/myrecipes
    localhost> cd ~/git/myrecipes
    localhost> git init
    Initialized empty Git repository in /home/larry/git/myrecipes/.git/

TODO: Push the repository to origin


Creating a Recipe
=================
We'll create a simple recipe, using your favorite text editor. This recipe will
be saved as ~/git/myrecipes/apple.yaml:

.. code-block:: yaml

    recipe_name: Giving an Apple to a Friend
    ingredients:
        - apple:
            amounts:
                - amount: 1
                  unit: each
    steps:
        - step: Give an apple to a fiend.

You may notice that this recipe contains an inconsistency. Don't worry about it,
we'll fix it up in just a moment. For now, we'll save the recipe, and then see
what git has to say about it.

.. code-block:: bash

    localhost> git status
    # On branch master
    #
    # Initial commit
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #   apple.yaml
    nothing added to commit but untracked files present (use "git add" to track)

Git can see that the file is there, but it's not currently tracking any changes
to it. Let's add it, and see what git thinks about it.

.. code-block:: bash

    localhost> git add apple.yaml 
    localhost> git status
    # On branch master
    #
    # Initial commit
    #
    # Changes to be committed:
    #   (use "git rm --cached <file>..." to unstage)
    #
    #   new file:   apple.yaml
    #

Git has now been notifed that `apple.yaml` is available to be added to the repo.
However, it has not yet been checked in (or "committed", as git calls it), and
so git is still not technically tracking changes to it. Let's go ahead and
commit it.

.. code-block:: bash

    localhost> git commit -m 'This is my first commit'
    [master (root-commit) 1617167] This is my first commit
     1 file changed, 8 insertions(+)
     create mode 100644 apple.yaml
    localhost> git status
    # On branch master
    nothing to commit, working directory clean

The `-m` option designates a commit message. This is usually a quick, one-line
message giving a brief overview of what changes have occurred between this
version and the previous version. With the first commit, it is usually
reasonable to just say, "First commit". Any changes after that should be
detailed enough that somebody in the future (who may be you) can easily identify
when certain changes were made. One way to remind yourself to do this, is to
assume that the next person to look at your work is a homocidal axe murderer
who knows who you are and where you live.

Git is now officially tracking changes to this file. But as you may have
noticed before, there is an error in the recipe. The title of the recipe is,
"Giving an Apple to a Friend", but the recipe itself states that the apple is to
be given to a fiend. After this typo has been corrected, we can check Git to see
how it is tracking our change.

.. code-block:: bash

    localhost> git diff
    diff --git a/apple.yaml b/apple.yaml
    index 72cd1a1..0ec3011 100644
    --- a/apple.yaml
    +++ b/apple.yaml
    @@ -5,4 +5,4 @@ ingredients:
                 - amount: 1
                   unit: each
     steps:
    -    - step: Give an apple to a fiend.
    +    - step: Give an apple to a friend.

The `git diff` command shows us the difference between the old version of the
file (`a/apple.yaml`) and the new version of the file (`b/apple.yaml`). The
format that it uses tells us that any line starting with `-` shows a line that
has been removed from the old version, and any line starting with `+` is a line
that was added to the old version. In this case, the following line:

.. code-block:: bash

    - step: Give an apple to a fiend.

Has been changed to this in the new version:

.. code-block:: bash

    - step: Give an apple to a friend.

With the change in place, we may now add and commit a new version of this file.

.. code-block:: bash

    localhost> git add apple.yaml 
    localhost> git commit -m 'Correcting typo: friend, not fiend'
    [master 4f59a41] Correcting typo: friend, not fiend
     1 file changed, 1 insertion(+), 1 deletion(-)

At this point, two different versions of the file exist in the git repo. This is
the important part of revision control: we can go back and look at old versions,
and compare how something is done now with how it was done before. This can be
especially important when doing recipe testing; somethings it helps to see how
a recipe has evolved over time.

Since we've left reasonable commit messages in git, we can go back and see, at a
glace, where certain changes were made.

.. code-block:: bash

    localhost> git log
    commit 4f59a41a9bc0e06f2858302ce3332d336140ca7f
    Author: Larry Fine <larry@stooges.com>
    Date:   Sat Jun 22 14:33:29 2013 -0600
    
        Correcting typo: friend, not fiend
    
    commit 824ba5bc2aa4cb07f33a82c9f1f833debb5fd055
    Author: Larry Fine <larry@stooges.com>
    Date:   Sat Jun 22 14:22:57 2013 -0600
    
        This is my first commit

You can see that log messages are displayed in reverse order (most recent
first). If we had enough entries that this output took up more than a single
screen, git would have automatically displayed it using the default paging
program on your system.

