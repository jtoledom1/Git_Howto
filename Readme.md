## First Steps Guide to Using Git and GitHub
### Index

1. [Initial Configuration](#initial-configuration)
2. [Merge](#merge)
3. [Stash](#stash)
4. [Git Alias](#git-alias)
5. [Git Tag](#git-tag)
6. [Git remote SSH Method](#git-remote-ssh-method)
7. [Fork and Pull Request](#fork-and-pull-request)

## Initial Configuration

Set up your username:

```bash
git config --global user.name "USER"
```

Set up your email:

```bash
git config --global user.email USER@example.com
```

### Switching the working branch:

```bash
git branch -m main
```

### Get information about the status

```bash
git status
```

### Add elements to stage for snapshot

```bash
git add FILE_NAME
```

You can also use a period at the end to indicate that everything that needs to be added should be added, especially if there are multiple files:

```bash
git add .
``` 

### Perform a commit (snapshot)

This will open a Vim editor where you'll manually enter the comment:

```bash
git commit
```

Perform a short commit (Don't forget the double quotes):

```bash
git commit -m "COMMENT"
```

*IMPORTANT NOTE*: Every time you want to make a commit, you must add items to the snapshot using `git add`.

### Revert to the previous saved version

```bash
git checkout HASH_COMMIT -- FILE_NAME
```

### To view the list of our changes, we can use the following commands

- `git log` (Extended version)
- `git log --graph` (Extended version with vertical line graph of changes)
- `git log --graph --pretty=oneline` (Shortened version of commit, includes full hash and comment)
- `git log --graph --decorate --all --oneline` (Shortened version of commit, includes abbreviated hash and comment)

### Git reset

- `git reset` (Deletes everything after the LAST snapshot)
- `git reset --hard HASH` (Deletes everything after the specified snapshot)
- `git reflog` (Gives you a history of changes)

To undo the `--hard`, enter `reflog` to see the hash and with a `checkout`, you can revert to a previous snapshot.

### Creating a shorthand method for commands

```bash
git config --global alias.ALIAS_NAME "log --graph --decorate --all --oneline"
```

This way, every time you call the alias, the command will be executed, for example:

```bash
git ALIAS_NAME
```

### Knowing if changes have been made, and it tells you what changes were made

```bash
git diff
```

## Git Alias

The short version of one or more commands:

```bash
git config --global alias.<alias_name> '!command1 && command2'
```

For example, to create an alias called "superpush" that pulls the main branch from origin and then pushes it to the same branch on origin, you can use:

```bash
git config --global alias.superpush 'pull origin main && push -u origin main'
```

## Git Tag

*Use snake_case*

Tagging a version:

```bash
git tag "name_1"
```

Move to a tag:

```bash
git checkout tags/class_1
```

## Git Branches

They are used to add features without modifying the main branch.

To create a new branch and add features without modifying the main branch:

```bash
git branch NAME
```

To switch to a specific branch:

```bash
git switch NAME
```

## MERGE

Bring changes generated in the main branch to the current branch:

```bash
git merge main
```

## Conflict Resolution

If the same line of code in the same file is modified, a CONFLICT is generated, and it shows both possibilities: the current change and the incoming one.

To check if we have conflicts before merging, we'll use a command seen previously:

```bash
git diff BRANCH
```

Previously used to compare files, but it also serves to compare branches.

## STASH

Make a temporary commit that is saved locally and not reflected in the general tree:

```bash
git stash
```

List stashed changes:

```bash
git stash list
```

Retrieve the stash:

```bash
git stash pop
```

When using `git stash pop`, you retrieve the information but it's not yet in the tree, meaning if you have to switch branches, you would have to repeat the steps: `git stash` and when you return to the original branch, `git stash pop` again. It's important to mention that you can perform the previous command from a different branch than where it was generated, and Git will interpret it as a merge.

Delete the saved information in the stash:

```bash
git stash drop
```

## Deleting Branches

Branches can be deleted as they lose their usefulness, i.e., when the changes are already unified with the main branch.

```bash
git branch -d BRANCH
```

## Adding features without modifying the main branch

Branches are used to add features without modifying the main branch.

### Creating a new branch

To create a new branch and add features without modifying the main branch, use the following command:

```bash
git branch NAME
```

## Switching to a specific branch

To switch to a specific branch, use the following command:

```bash
git switch NAME
```

## Git remote SSH method

### Starting with an existing repository and combining local progress with GitHub:

1. Add the remote origin to the local repository:

```bash
git remote add origin git@github.com:USER/Git_Howto.git
```

2. Add modified files to the staging area:

```bash
git add .
```

3. Commit with a descriptive message:

```bash
git commit -m "Commit message"
```

4. Fetch remote changes and merge them with local changes:

```bash
git pull origin main --allow-unrelated-histories
```

5. Configure rebase option for future pulls:

```bash
git config pull.rebase false
```

(Recommended to use this only in the beginning)

6. Push local changes to the remote repository:

```bash
git push -u origin master
```

### Starting from scratch with an existing repository:

To start working from scratch with an existing repository, simply clone it into the folder where you want to store your local repository:

```bash
git clone git@github.com:USER/Git_Howto.git
```

### Making commits and pushes:

Every time you want to make a commit and push, follow these steps:

1. Add modified files to the staging area:

```bash
git add .
```

2. Commit with a descriptive message:

```bash
git commit -m "MESSAGE"
```

3. Fetch remote changes and merge them with local changes:

```bash
git pull origin main
```

4. Push local changes to the remote repository:

```bash
git push -u origin main
```

## FORK and PULL REQUEST

### Forking the repository

1. Go to the GitHub repository you want to fork.
2. Click on the "Fork" button in the top right corner of the page.
3. Select your account as the destination for the fork.

### Cloning the forked repository

Once you have forked the repository, clone the repository to your local machine:

```bash
git clone FORKED_REPOSITORY_URL
```

### Making changes and pushing them to the cloned repository

1. Make necessary changes in the cloned files.
2. Add the modified files to the staging area:

```bash
git add .
```

3. Commit with a descriptive message:

```bash
git commit -m "Description of the changes"
```

4. Push the changes to the forked repository on GitHub:

```bash
git push origin BRANCH_NAME
```

Here's the translation:

### Creating a pull request

1. Go to the forked repository on GitHub.
2. Click on the "Pull Request" button at the top.
3. Provide the necessary information for the pull request, such as a detailed description of the changes made.
4. Click on "Create pull request" to submit the request to the original repository.

There you go! You have forked a repository, cloned the fork, made changes, and sent a pull request to the original repository.

<a href="https://github.com/jtoledom1/Git_Howto/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=jtoledom1/Git_Howto" />
</a>

Made with [contrib.rocks](https://contrib.rocks).
