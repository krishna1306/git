# Bisect - To find bugs

If you have a bug in a specific commit and if you already know a good commit, you can let `git` help find out where the bug was introduced.

```bash
# Enter the bisect mode
git bisect start

# Tell git that the current commit is a bad commit
git bisect bad

# Tell git about a good commit
git bisect <good-commit-id>
```

After this, `git` moves the head to the first point of inspection (detatched head state) - typically half way point of all commits

- Now, run the automated tests to see if the issue (bug) is present or not
- If not present, you just eliminated half of commits

```bash
# Tell git that this new HEAD point is a good commit
git bisect good
```

- Continue doing this until you land on the "bad" commit and have **no revisions** left

Now, git moves "head" to the good commit (the one just prior to bad commit)

```bash
# This is the last time you will enter "bad" commit
git bisect bad
```

The output will show

- Author
- Email
- Commit message
- Commit ID
- `--stats` showing the files and the number of changes in each file

#### End the bisect mode

End the bisect mode by resetting the **HEAD** pointer

```bash
git bisect reset
```

### Visualise the commits and where the head is

```bash
git log --oneline --all
# "--all" is necessary as we are in detatched HEAD state
```

