# Git

Welcome to today's lecture on Git, presented by Anna Hsu and Daniel Chua, Co-President and Lecturer, respectively, of TJ Dev Club. Feel free to follow along with the presentation [here](https://docs.google.com/presentation/d/1j5NSsMaTRWZ-llJAPguyrm7CfhmcmuP2zTEwrw2te7Q/edit?usp=sharing).

## Introduction

Git is a version control system that was launched in 2005 that developers around the world use today.

### Version Control

Why should you care about version control? It’s a way for people to keep track of their code and files. If you screw up your code or you accidentally delete it, you have an old copy you can refer to. This isn't unique to code—for example, Google Docs has “Version History” where you can refer to old versions and revert, or go back, to it. In the case of Git, if the computer with your code caught on fire, you’d be able to recover your entire project and the whole history behind it, using the version control to act as a full backup of your project in a Git directory, or folder. This full backup happens every time you engage with Git.

Git is also a handy tool for collaboration, since everyone can share code that’s working on the same version. Think about how you’re able to edit a document at the same time as a friend on Google Docs!

### Three States

Your files can be in three states when you’re working with Git: **modified**, **staged**, and **committed**. These are tracked files, which are files Git knows to snapshot. When a file has been modified, it means that you’ve made and saved changes to a file but nothing beyond that has been done. There’s a staging area is a place that lists out what will go into your next commit. When a file has been staged, a modified file is prepared to be committed. Lastly, when a file has been committed, a snapshot of the modified file has been taken, saved in your Git directory, and moved out of the staging area.

What happens when you’ve just created a new file—it’s not in any of these three states, right? You’re correct, since Git won’t track a file unless you explicitly tell it to. In this case, it is considered **untracked**, and you’ll learn how to add untracked files later in the lecture.

![Three Stage Visualization](./images/threestages.png)

### How To Use Git

There are two ways to use Git: through the command line and a GUI. We won’t be using the GUI because it doesn’t have all of the features of Git, so we’ll leave you to explore that on your own if you’re interested.

### Command Line

Some of you might not have ever used the command line before, and that’s okay! The command line is just an interface where you can run commands. While you’re using it, you don’t need to know how to use it in depth. There’s really only one command that’s critical in using the command line with Git: `cd`. You use this command to switch directories, or folders. When you open your command line, you’ll want to navigate to the folder with your Git directory, so you’ll be using this to get there.

If you want to find out more about the command line or Linux, I recently gave a presentation on Linux at Computer Security Club, so feel free to check it out [here](https://docs.google.com/presentation/d/1uIMQZC4ej3zu8Y73CJgVRZwDcDU6AVQqbh06nEdlUSk/edit?usp=sharing).

### Git vs. Github vs. Gitlab

Let’s talk briefly on the differences between Git, Github, and Gitlab. Git, as we’ve mentioned, is a version control software that’s involved on a local scale. On the other hand, Github and Gitlab are cloud services that host Git repositories, which is what enables the collaboration element of Git. Most people start out on Github, since it’s generally considered more popular. Part of this is because Microsoft owns Github now, while Gitlab is open source. There are pros and cons to both, which we won’t go over in this lecture, since we’ll be focusing on using Git on Github.

## Setup

Git requires a bit of setup, so let’s go over how to do it!

### Installation

Installation of Git depends on the platform you’re on. If you’re on a personal computer, follow the install command or link for the platform your computer uses. If you’re on a school laptop, go to Director, create a new site, and add git `openssh-client` to your list of packages when configuring your Docker image. We’ll get into how to use Git on Director in a bit, since it’s a little bit more involved.

- Linux: `sudo apt install git-all`
- macOS: `git --version`
- Windows: `https://git-scm.com/download/win`

### Github Account

To use Github, sign up for an account at <https://github.com/>. You can get extra privileges if you also apply for the [Github Student Developer Pack](https://education.github.com/pack), although since the Sysadmins have stopped email service, we're not 100% sure if you'll be able to gain access.

### Configuration

Before you get started with using Git locally, you have to configure it so that it knows your name and email through the first and second commands listed. Use the name and email that you have on Github for consistency’s sake. This information will reside in a `.gitconfig file`, which you can check with the third command listed.

```
git config --global user.name "<your name>"
git config --global user.email <your email>
git config --list --show-origin
```

### SSH

To connect your local Git repository and Github, we’ll be using SSH keys. You generate one, following the [instructions](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) Github has provided for your computer’s platform, and you’ll add it to Github. Contact an officer if you require assistance.

## Git Commands

### Help Commands
A lot of the commands we’ll be going over might be new and/or confusing to you. Thankfully, there are a few ways that you find out how a command works. On Linux, you can use the manual pages command through `man <command>`. You can also use `git <command> --help` on any platform with Git installed.

### Set Up a Repository

There are two ways to set up a repository: using an existing local repository or cloning an existing Git repository. You can set up a new Git repository locally by using `git init` in the directory you want to turn into a Git repository. You can also create a Git repository on Github’s website for you to clone, or you can fork someone else’s repository to your own account. You can clone it by hitting the “Code” button, copying the SSH link, and using `git clone <SSH link>`.

Note: Github doesn’t really support HTTPS cloning anymore.

### Recording Changes

After you’ve set up your Git repository, you can start tracking the version history of your files. If you’ve already created some files in your Git repository, if you run git status, it will tell you that your files are “untracked.” This means that Git is not currently tracking these files because you haven’t committed them yet to the “version history.” When you’re working on a project with lots of files, it can get hard to keep track of which ones you’ve committed and which ones you haven’t which can be problematic. git status will report which files haven’t been “saved” (committed) to the version history yet so you don’t forget to save important code! This report includes files that are untracked as well as staged.

Once you are ready to commit changes to a file, you have to stage it first. In order to stage a file that’s untracked or modified, we use `git add <name>` (the name of the file including the file extension), to “add” it to the stage. Typing out git add for each individual file is annoying, though, if you have a lot of files you want to commit, so if you want to stage all the untracked/modified files in the current directory, instead of typing the file name after `git add`, type a period (`.`) which represents the current directory. Make sure that the files you’re tracking are all files you want, though! Later, we’ll teach you the best practices for telling apart what you should have and what you shouldn’t.

Once you are ready to commit, just type `git commit -m <message>` with a brief description of your commit within the quotes. For longer commit messages, you can type `git commit` and it will allow you to format text more easily. If you are using longer commit messages, once you’re done editing press `ESC` to get out of `Insert` and type `:wq` to exit the text editor. If you really want a shortcut, although this isn’t necessarily recommended, you can use `git commit -a -m <message>` to do `git add .` and `git commit -m <message>` all in one step. Aim to have the shortest yet most d`escriptive commit message, so if you ever have to look back on the work you did, you’ll know exactly what you changed. Once you’ve committed, this snapshot of your repository is saved to the version history.

### Undoing Changes

Conveniently, Git also gives you ways to undo changes, which can be helpful if you’re prone to either compulsive commits or screwing things up. (Speaking from experience.) If you’ve staged a file, but you want to unstage it, you can use `git restore --staged <file>`. If you want to go a step further and remove all of the modifications you’ve made in the file and return to the last snapshot, you can use `git restore <file>`. There are old versions of these commands in previous version of Git, so just be aware if you come across it in tutorials or documentation. If you’ve already committed, you can “edit” the commit message of the last commit you’ve made through  `git commit --amend`.

### Reviewing Commits

If you want to look at your previous commits, you can use `git log`. This will provide you a list of all the previous commits with information about each individual commit such as who committed, when they committed, the description of their commit, and other things like the commit’s SHA which is basically a string of characters that uniquely identifies the commit like your FCPS ID would identify you.

### `.gitignore`

While you’ll likely want to commit most of the files in a certain project to your Git repository, there are some files you should leave out, and you’ll do so within the `.gitignore` file. There are a variety of [official online templates](https://github.com/github/gitignore) for most projects, provided by Github, so you can always start there.

If you’ve already committed a file to your repository but it should actually be ignored, you can use `git rm --cached <file>` to remove it.

### Branching

With branching in Git, you’re able to, in a sense, duplicate a set of commit snapshots and make changes on them. At the same time, if you need to deploy a fix elsewhere in your code, you can do it on a different branch and deploy it without having to deploy or revert your other changes.

Here’s an analogy: let’s say you’re working on a multi-stage project for a class. You’ve submitted a copy to your teacher for a part to grade, and you’ve made a copy to work on for the next part. However, your teacher has updated the rubric for the last part you’ve submitted, so you open the one you’ve submitted to them and you make your changes. You don’t have to show them your new changes for the next part of the project, but you also don’t need to delete them, because it’s on a different copy. In the end, you can copy paste your project into the original file that you submitted to your teacher.

That’s how Git branching works, in a sense. You make a new branch, which is like the new copy, using `git branch <name>`, and you move to that branch using `git checkout <name>`. (For a shortcut, you can use `git checkout -b <name>` to do both steps in one step.) You can then make changes on that branch without worrying about your main branch having changes you don’t want to deploy yet.

This will become more important when we talk about deployment in our next lecture.

### Merging

When you’ve finished your changes on your branch, it’s time to merge back in to your main branch! First, switch to your main branch, then use `git merge <branch>` to merge your branch. When the files that you’ve modified in your updated branch are the only modifications in those files, then they’ll be fast-forwarded, which means that the pointer for the main branch is moved up and you’re all set.

However, sometimes there are conflicting modifications in branches, meaning that you’ll have to do some extra work. You’ll have to resolve the merge conflicts. You can choose the modifications made by one branch or the other, or pick and choose yourself in your text editor. After you’re done, you can commit your changes.

### Remotes

You’ve been working locally this whole time, but what if you need to work with other people on a project? In this case, Github hosts your remote, and you can check your remotes by running `git remote -v`. If you’ll ever need to add a remote to your repository, use `git remote add <shortname> <url>`. For repositories that you own, such as forks, you should have both fetch and push remotes set up by `git clone`. To get changes from the remote (such as when someone else you work with has updated the repository), use `git pull`, and to bring changes you’ve made to the remote, use `git push`.

### Pull Requests

Now that your fork is up to date with the work you’ve made locally, you can make a pull request to the original repository you forked from to propose your changes and generate discussion over your proposal. To create a pull request with a fork, go to the “Pull requests” tab in the Github repository. Click the green button that says “New pull request” and the link that says “compare across forks.” Select the branches and forks that you want to compare, and make your pull request. You can request reviewers, add tags, etc. Someone else in charge of the repository will come look at your code!

## Additional Resources

There is a plethora of resources online that you can use to learn and use Git!

- [The Git Book](https://git-scm.com/book/en/v2)
- [1 hour FreeCodeCamp tutorial](https://www.freecodecamp.org/news/git-for-professionals/)
- [Creating the Perfect Commit™️](https://css-tricks.com/creating-the-perfect-commit-in-git/)
- [Cheatsheet!](https://about.gitlab.com/images/press/git-cheat-sheet.pdf)
- [`.gitignore` templates](https://github.com/github/gitignore)

## Any questions? Feedback?
Congrats on making it this far! Let me know if you have any questions about anything we've covered in this presentation, and don't hesitate to reach out if you have any feedback!
