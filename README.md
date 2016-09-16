# Git-Cypt Instructions

- Install [Git-Crypt]
```sh
brew install git-crypt # OSX
apt-get install git-crypt # Ubuntu/Debian
```
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
- Add files to your encryption directory
- Git add and commit the files
```
git add -A
git commit -m "Added some files to be encrypted"
```
- At this point you should still be able to read the contents of the files in the encrypted directory; You can lock them with:
```
git-crypt lock
```
- The files in the encrypted directory should all now be encrypted
- Unlock the files again with `git-crypt unlock <path_to_keyfile`
```
git-crypt unlock ./crypt_key
```

## NOTES
- You must have a clean working directory (git) in order to lock or unlock encrypted files.
[Git-Crypt]: https://www.agwa.name/projects/git-crypt/
