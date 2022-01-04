# Browsing History

```bash
git log

git log --oneline
```

### See the statistics of changes in each commit

```bash
git log --oneline --stat
git log --stat
```

Example of how `--stat` would look

```bash
kribandi@KRIBANDI-M-X0Q2 Venus % git log --oneline --stat
a642e12 (HEAD -> master) Add header to all pages.
 audience.txt                                    | 4 +++-
 objectives.txt                                  | 1 +
 sections/creating-snapshots/init.txt            | 2 +-
 sections/creating-snapshots/staging-changes.txt | 2 +-
 toc.txt                                         | 2 +-
 5 files changed, 7 insertions(+), 4 deletions(-)
50db987 Include the first section in TOC.
 toc.txt | 6 +++++-
 1 file changed, 5 insertions(+), 1 deletion(-)
```

### See the exact changes in each commit

```bash
git log --oneline --patch
```

Example of how `--patch` would look

```bash
a642e12 (HEAD -> master) Add header to all pages.
diff --git a/audience.txt b/audience.txt
index 6b3f8f5..4cfef55 100644
--- a/audience.txt
+++ b/audience.txt
@@ -1,2 +1,4 @@
+AUDIENCE
+
 This course is for anyone who wants to learn Git.
-No prior experience is required.
+No prior experience is required.
\ No newline at end of file
diff --git a/objectives.txt b/objectives.txt
index d31b40a..c882718 100644
--- a/objectives.txt
+++ b/objectives.txt
@@ -1,3 +1,4 @@
+OBJECTIVES

 By the end of this course, you'll be able to
 - Create snapshots
```

**patch** shows the diff of each file in each commit

## Filter History

You can filter by

- Author
- Date
- Commit message
- Content etc.,

```bash
# See the last 3 commits
git log --oneline -3

# Filter by author
# Partial name is enough
git log --oneline --author="Krishna"
```

### Filter using dates

```bash
# AFTER a given date
git log --after="YYYY-MM-DD"

# BEFORE a given date
git log --before="YYYY-MM-DD"

#---------- Using Abstract References -----------#
# Yesterday
git log --after="yesterday"

# One week ago
git log --after="one week ago"
```

### Filter by commit message

```bash
# Search term is case-sensitive
git log --grep="GUI"
```

### Filter by commit contents

```bash
# Find all the commits that added or removed the word "OBJECTIVES"
git log -S"OBJECTIVES"
```

### Find all commits between given two commits 

```bash
git log --oneline <commit-id-start>..<commit-id-end>
```

### Find all commits that modified a specific file

```python
# See all the commits that changed the file toc.txt in some way
git log --oneline toc.txt

# If GIT complains about the file, insert an empy KWARG
git log --oneline -- toc.txt
```

### Pretty Format the log output

```bash
git log --pretty=format:"%Cgreen%an%Creset committed %H on %cd"
```

`%Cgreen` -- color green from this declaration onwards

`%Creset` -- color reset

`%an` -- author name

`%H` -- long hash of the commit

`%h` -- short hash of the commit

`%cd` -- commit date

> Its better to set-up aliases for long `git` commands

#### Alias within git command

```bash
git config --global alias.lg "--pretty=format:'%Cgreen%an%Creset committed %H on %cd'"
```

Here the `lg` is the alias.

To use it - `git lg`

### See changes from COMMIT-X to COMMIT-Y

**COMMIT-X** is in the past

**COMMIT-Y** is in the furture

```bash
git diff HEAD~2 HEAD

# To see a specific file's diff between two commits
git diff HEAD~2 HEAD objectives.txt
```

### Checkouts (restore from a specific commit)

Sometimes you want your code to go back to a specific commit (in your working directory) - that's when you want to do a **check-out**

```bash
git checkout <commit-id>
```

> This results in a **detatched head** state

**Do not make any new commits in a "detatched head" state**

```bash
# To see logs from the new HEAD
# Same command as before
git log --oneline

# To see all logs (like before)
git log --oneline --all
```

Do **`git checkout master`** to go back to `MASTER` branch - after this, you can continue to do commits
