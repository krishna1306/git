# GIT

```bash
# Get GIT version
git --version
```

## Customise GIT environment

All the settings for GIT can be applied in one of the three levels

1. SYSTEM - All users
2. GLOBAL - All repos of the current user
3. LOCAL - Current repo

```bash
git config --global user.name "Krishna Bandi"
git config --global user.email krishna@krishna.com

# "--wait" makes git wait until new VSCode instance is spun
git config --global core.editor "code --wait"

# Edit all global settings in a visual editor
git config --global -e 
```

### Handling CR and LF

CR - Carriage Return `\r`

LF - Line Feed `\n`

```bash
# On Windows
# to remove "\r" when pushing to remote repo
# to add "\r" when pulling from remote repo
git config --global core.autocrlf true

# On Mac
# to remove "\r" when pushing to remote repo (even if the text editor adds by mistake)
git config --global core.autocrlf input
```

### Set Diff tool to GUI (optional)

```bash
# "vscode" is just a name
# Whichever name you use here must be used in the subsequent command too
git config --global diff.tool vscode

# "--wait" = wait until we close the VSCode (once launched)
# "--diff" = we want to use vscode for diff
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"
```

