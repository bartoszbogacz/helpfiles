# GIT

```bash
git fetch -p
git branch -v
git branch -D ...
git show origin/afl-master:config/imports
git remote set-url --push origin ssh://i545846@hdbgerrit.wdf.sap.corp:29418/afl
```

On Linux `vim ~/.gitconfig`.

```gitconfig
[user]
	email = bartosz.bogacz@mailbox.org
	name = Bartosz Bogacz

[init]
	defaultBranch = main

[pull]
	ff = only

[core]
	editor = vim
```

On Windows `vim %USERPROFILE%\.gitconfig`.

```gitconfig
[user]
	email = bartosz.bogacz@mailbox.org
	name = Bartosz Bogacz

[init]
	defaultBranch = main

[pull]
	ff = only

[core]
	editor = 'C:\\Windows\\vim.bat' -i NONE
```
