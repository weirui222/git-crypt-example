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
- Create a pgp key
  - If you haven't worked with pgp keys before, I would suggest signing up with [keybase.io](https://keybase.io/) and using their tooling for this as they walk you through the process and allow you to store the pgp key with them so that you don't have to worry about losing it
- Make sure your private key gets added to your gpg keychain
```
# If you used keybase to create your key and you installed the keybase app, you can export it with:
keybase pgp export -s -o ~/Downloads/private.key

# Import it into your gpg keychain
gpg --import ~/Downloads/private.key

# Remove the private key file
rm ~/Downloads/private.key
```
- Add git-crypt collaborator
```
git-crypt add-gpg-user <keybase.io username or pgp public key>
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

- To be added, send your keybase.io username or your pgp public key to someone, who is already been added as a git-crypt user on this project, to add you as a git-crypt collaborator; The details section has the commands that an existing git-crypt user needs to run to add a new user
  <details>

  ```sh
  # This command can only be run by someone who is already been added as a git-crypt user on this project
  # Follow KeyBase user
  keybase follow USER_NAME
  # Import keys from KeyBase
  keybase pgp pull
  # List all gpg keys
  gpg --list-keys
  # USER_ID can be key id, full fingerprint, or email address associated to pgp key
  git-crypt add-gpg-user --trusted USER_ID
  ```
[Git-Crypt]: https://www.agwa.name/projects/git-crypt/
