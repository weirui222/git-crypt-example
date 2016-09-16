# Git-Cypt Instructions

- Install [Git-Crypt]
- Move into the root of your repo and initialize git-crypt
```
cd repo
git-crypt init
```
- Add this .gitattributes file to the directory you want encrypted
```
* filter=git-crypt diff=git-crypt
.gitattributes !filter !diff
```

[Git-Crypt]: https://www.agwa.name/projects/git-crypt/
