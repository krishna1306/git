# GIT Snapshots

## Initialise empty repo

```bash
git init
```

This creates `.git` hidden directory that contains all working files of **git**

## Workflow

Files ----> Staging Area ----> Commit

### Add files to staging area

```bash
git add file1 file2
```

### Commit

```bash
git commit -m "Initial commit"

# For longer commit messages
# It automatically opens the default text editor
git commit
```

> Even after committing, staging area still contains all the files we put there

Staging area ----> should contain code that we intend to put in production

**Any file we modify** --> `git add <file>` Add it to staging area before committing

**Even the file we delete** --> `git add <file>` **Git** will delete the file from the staging area too.

## Staging Area

### See the status and staging area

```bash
git status

# Short notation
# Contains two columns in the left
# |1|2| -- 1 ==> Represents Staging Area
# |1|2| -- 2 ==> Represents Working directory
git status -s

# To just see the files in the staging area
git ls-files
```

If the contents of our working directory is the same as what we have in staging area (which inturn is the same as the last committed data -- **Its all good**)

### Check the `diff` between Staging area and Previous Commits

```bash
git diff --staged
```

This command compares all the data in the **previous commit** (file 'a') with the data in the **staging area** (file 'b').

A command like `diff -git a/file1.txt b/file1.txt` will be called for each file in the staging area.

Output of the diff file can be too long based on how many files are there and how long each file is.

Each chunk in the `diff` output has a header that looks like `@@ -1,3 +1,5 @@`

`-1,3` means --> lines `1` to lines `3` were in the previous commit (file 'a') - also indicated by `-`

`+1,5` means --> lines `1` to lines `5` were in the staging area (file 'b') - also indicated by `+`

### Check the `diff` between Working Directory and Staging area

```bash
git diff
```

### If `difftool` is configured

Refer to **git_part_1.md** to find out how to configure **difftool**

```bash
# Show the diff in vscode -- Staging Area vs Working Directory
git difftool

# Show the diff in vscode -- Repository vs Staging Area
git difftool --staged
```

### Skipping the staging area

**Not Recommended**

```bash
git commit -a -m "Some commit message"
```

### Remove a file - both from Staging area and Working directory

```bash
# Instead of "rm" use "git rm"
git rm file1.txt
```

### Rename a file - for both Staging area and Working directory

Similar to `rm` **git** also has special `mv` command

```bash
git mv file1.txt file2.txt
```

If you don't use `git mv` then each file rename requires two `git add` operations

1. One operation of `git add` to add the renamed file (file with a new name is like a new file)
2. Another operation of `git add` to add the old file - which `git` will remove then from staging area

## Ignoring Files

Create a file **`.gitignore`** in the project directory

Just put all the directories and files (paths) inside it 

> Paths must be relative to the project directory

For example, to ignore **logs** directory in the project, just add

```bash
logs/

# Use patterns
*.logs

# For a specific file
main.log
```

After this, add `git add .gitignore` and then `git commit -m "commit message"`

> This will ONLY WORK when the file/directory to be ignored is not yet tracked with git

To ignore a file or directory that is already being tracked, you need to remove it from staging area

```bash
# "-r" --> recursive removal
# "--cached" --> represents the staging area
git rm -r --cached bin/

# Commit the new staging area to the repo once again
git commit -m "Remove the bin directory that was accidentally committed"
```

## Unstaging Files

Unstaging = Undo of `git add`

```bash
# "restore" command is available only in the recent versions of git (>2.28.0)
git restore --staged file1.txt

# To restore all files from staging area
git restore --staged .
```

**What does unstaging do - in the background?**

`git` will simply get a copy of the unstaged file (if present) from the previous commit and puts it in the staging area

If you think about it, before you did `git add` - staging area and the previous commit were in **sync**

## Discarding Local Changes

What if you don't like the changes in the working directory itself? 

You can simply discard all changes to a file (or a set of files) in the working directory and replace it with a copy from staging directory (the next environment)

Working Directory (Env) --> Staging Area (Env) --> Repo (Env)

```bash
git restore file1.txt

# To restore all
git restore .
```

> `git` cannot restore untracked files

## Clean untracked files

```bash
git clean

# To force 
git clean -f

# To force clean including directories
git clean -fd
```

Whenever we use `git clean` - we use it with `-fd` options generally

## Logging in Git

```bash
git log

# See one line description of each commit
git log --oneline

# Reverse the order of display
git log --oneline --reverse
```

## See the data in commits 

When you want to see the exact data present at the time of a specific commit you use `git show` command

#### To see the `diff` between current commit and an old commit

```bash
git show <commit-id>

# You can also use "HEAD" pointer
git show HEAD

# You can also fetch commits relative to "HEAD"
git show HEAD~1
```

#### To see the content itself - not the `diff`

```bash
git show <commit-id>:<file-path-relative-to-project-directory>

# Example
git show 912ab42:bin/app.js

# You can also use HEAD or relative HEAD
git show HEAD:<fpath>
git show HEAD~1:<fpath>
```

### See all files and directories in a commit

```bash
git ls-tree <commit-id>
```

Each file is called a `blob`

Each directory is called a `tree`

You will also notice unique IDs given to the files and directories in that commit

```bash
# See the content of a file or directory using the Unique ID
git show <content-id>
```

## Restore the file to its previous version

`git restore` command will restore a file from the next environment.

- If you restore a file in working directory, it will be picked from staging area
- If you restore a file in staging area, it will be picked from last commit

To change this behavior, you can also specify the environment (commit) from which to restore the file

```bash
git restore --source=HEAD~1 file1.txt
```





888-550-4427

924-801-7202