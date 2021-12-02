1. Initialise the GIT repo
2. Configure Files to track
   1. Git tracks changes
3. Stage changes
4. Commit changes

---

```
yum install git -y
```

---

### Set-up user

```
git config --global user.email "your@example.com"
git config --global user.name "Your Name"
```

---

### Start with `git` 

```
git version

# Initialise an empty repo
git init

# List of untracked files
git status

# Add files for tracking
git add <file1> <file2> <file3> ...

# Stage for changes
git add <file-to-be-staged>

# Commit changes
git commit -m "Initial message"
```

