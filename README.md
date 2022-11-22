# gpgUtils
A package of utilities that work along-side GPG.

Utility can sign and encrypt files via drag / drop functionality. Also includes features to automatically configure your installed copy of `gpg` to work alongside of PuTTY  / Yubikey.



## Requirements
This project currently requires the following:
- **Windows** based machine ( Windows 7 SP1 or greater )
  - To make use of `Powershell` for Yubikey setup
- **Gpg4win**
  - Can be installed from within the utility itself 



## Setup / Configure
- Download gpgUtils
- Extract to a location on your computer
- Open `cfg\config.ini` in a text editor
- Locate `gpg_keyid=` and enter your gpg key_id



## How to Use
Once you have downloaded / extracted gpgUtils to your computer; find a file you wish to encrypt or sign and `drag / drop` the file(s) onto `gpgUtils.exe`.

The utility will automatically open and present you with a list of options.

Once you have encrypted / signed your file(s); they will be placed in the `output` folder.



## Features
### GPG Quick Menu
- **Sign only**
  - Signs a file with your configured GPG key.
  - Armored _(optional)_

- **Encrypt Recipient**
  - Signs + Encrypts a file to another person by providing a key_id or email address
  - You must have recipient's public key imported into your GPG program
  - Armored _(optional)_

- **Encrypt Self**
  - Signs + Encrypts a file to yourself using your specified key_id.
  - Armored _(optional)_

- **Encrypt + Symmetric**
  - Creates an Encrypted + Symmetric file
  - Symmetric files allow a person to decrypt with key_id OR passphrase.
  - Armored _(optional)_
  - Sign _(optional)_

- **Symmetric**
  - Creates a Symmetric file (no encryption)
  - Supports specifying a different algorithm to use:
    - IDEA
    - 3DES
    - CAST5
    - BLOWFISH
    - AES
    - AES192
    - AES256 _(default)_
    - TWOFISH
  - Armored _(optional)_
  - Sign _(optional)_
  
- **Detached**
  - Creates a Detached signature from a specified file
  - Armored _(optional)_

- **Clearsign**
  - Creates a clear-signed file.
  - Supports alternative hash methods:
    - SHA1
    - SHA224
    - SHA256 _(default)_
    - SHA384
    - SHA512
    - RIPEMD160
  - Armored _(optional)_

- **Custom** _(user specified)_
  - Walks user through step-by-step asking which options to use.
  - Allows user to enable any number of combinations instead of the strict options above.

### Advanced
- Download GPG4win
- Restart GPG Services
- Run Kleopatra
- Open GPG Folder
- scdaemon.conf (open file)
- scdaemon.conf (automatically configure for yubikey)
- gpg-agent.conf (open file)
- gpg-agent.conf (automatically configure for yubikey / ssh / putty)
- Detect Yubikey
- Install / Run PuTTY
- GPG4win website



## Notes
### Symmetric
When speciying which algorithm you wish to use; certain algorithms may return:
```shell
Invalid cipher algorithm
```
This error occurs when your computer does not have libraries installed for that specific algorithm.



### Locating your GPG key _id
Once you have installed `Gpg4Win`, you will need to generate the keys you will use to sign / encrypt your files with.

After you've created your keys, open `Command Prompt` or `Windows Terminal` and execute:

```
gpg --list-secret-keys --keyid-format=short
```
You will be shown a list of available keys:

```ini
sec   rsa4096/ABCD1234 2022-11-14 [C]
uid         [ultimate] Username <youremail@address.com>
ssb   rsa4096/DEFA1234 2022-11-14 [S]
ssb   rsa4096/1234ABCD 2022-11-14 [E]
ssb   rsa4096/DCBA4321 2022-11-14 [A]
```
Copy the `key id` for the key you wish to use. The primary key is listed at the top to the right of `sec` and has a key_id of `ABCD1234`.

Your config file `cfg\config.ini` should be setup similar to the following:

```ini
gpg_keyid=ABCD1234
```

If you have your keys generated with subkeys like the example above; when you encrypt a file using gpgUtils, you can manually enter the key_id you wish to use at the time that you sign/encrypt a file.



## Future Versions (MacOS, Linux, etc)
At present; this utility is available as a Windows executable.
I have plans to transfer this project over to the programming language `GO`so that builds can be made for macOS and Linux, but this is heavily dependent on available time.

## Todo
- Add ability to support verify, decrypt, and numerous other GPG features
- Migrate project over to GO programming language.
  - Support for Linux / MacOS
