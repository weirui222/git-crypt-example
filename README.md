# Git-Crypt Instructions
These instructions are for setting up git-crypt in symmetric mode so there will be a single key that ecrypts and decrypts your files. 

- Install [Git-Crypt]
```sh
# OSX
brew install git-crypt

# Ubuntu/Debian
apt-get install git-crypt
```
- Move into the root of your repo and initialize git-crypt
```
cd repo
git-crypt init
```
- Export the encryption key and make sure to keep it safe; It should only be given to people whom you want to give access to your secrets; The encyrption key should **NOT** be stored in your repo; It was only stored in this repo as an example
```
git-crypt export-key <path_to_keyfile>
```
- Add this .gitattributes file to the directory you want encrypted; The "*" says encrypt everything in this directory. You can use wildcards to match specific files or directories.
```
 * filter=git-crypt diff=git-crypt
 .gitattributes !filter !diff
```
- Add files to your encryption directory
- Git add and commit the files; Your git working directory must be clean (no unstaged/uncommited files) in order to encrypt or decrypt files
```
git add -A
git commit -m "Added some files to be encrypted"
```
- At this point you should still be able to read the contents of the files in the encrypted directory; You can lock them with:
```
git-crypt lock
```
- The files in the encrypted directory should all now be encrypted
- Unlock the files again with `git-crypt unlock <path_to_keyfile>`
```
git-crypt unlock ./crypt_key
```

[Git-Crypt]: https://www.agwa.name/projects/git-crypt/
