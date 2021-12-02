`push` to remote repository

`pull` from remote repository

Git server is also part of `git` application and is handled by `git` daemon.

_Make sure that remote repository is created on **github.com** and URL is generated for that repo_

```
git remote add <name> <url>

git remote add github <url>
```

`name` can be any name - for local reference to identify the remote repo uniquely 

`url` points to the repo URL on `github` for example.

```
git push <name> <branch>

git push -u github master
```

`-u` - because `master` is not created on the remote repo yet

---

**Clone** the repo first from a remote repo.

```
git clone <url>
```

Since you just `clone` a repo, you don't need to add `remote` again. `git` is smart enough to just use the URL you used for `clone` to be used for `remote` too.

_What about the `remote` name then?_

A name called **origin** is used for such auto additions (default name)

Origin -> Original

---

```
git pull 
```

`pull` only pulls the latest changes.