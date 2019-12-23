# pass ssh 0.1 [![build status][build-img]][build-url]

A [pass](https://www.passwordstore.org/) extension that creates ssh
keys with an automatically generated passphrases stored in pass and
outputs the public key using [fzf](https://github.com/junegunn/fzf) or
[rofi](https://davedavenport.github.io/rofi/).


## Use case

The examples suppose you use the
[`xclip`](https://github.com/astrand/xclip) clipboard manager:

### Create a new ssh key

Run `pass ssh`, this will show all existing keys under `~/.ssh`.
Create a new one by entering the name of a key that does not exist,
for example `mynewkey`. `pass ssh` will then generate a new password
for it in the password store under `/sshkey-passphrase/mynewkey` and
use that passphrase as the ssh key's passphrase. Finally, `pass ssh`
will output the ssh key's public key on stdout.

### Use the new ssh key

Connect to a host using the ssh key, for example `ssh -i
~/.ssh/mynewkey myhost`. `ssh` will then ask for a passphrase, the one
stored in the password store at `/sshkey-passphrase/mynewkey`. You can
then simply copy the passphrase with `pass --clip
/sshkey-passphrase/mynewkey` and copy paste it to the `ssh` passphrase
prompt.


## Usage

```
pass ssh [--help,-h]
    [--fzf,-f]|[--rofi,-r] [--ssh-dir <s>,-d <s>]
    [--pass-prefix <s>,-p <s>] [--passphrase-no-symbols,-n] [--passphrase-length <s>,-l <s>]
    [--ssh-t <s>] [--ssh-b <s>]
```

`pass-ssh` provides an interactive solution to create ssh private and
public keypairs with passphrases stored in `pass` as well as write the
public key to stdout. It will show all available ssh keys in either
`fzf` or `rofi`, wait for the user to select one and write the public
key to stdout.

The user can select `fzf` or `rofi` by giving either `--fzf`
or `--rofi`. By default, `rofi` will be selected and
`pass-ssh` will fallback to `fzf`.

If the selected key file does not exist under the directory given by
`--ssh-dir`, first a passphrase will be generated in `pass`
under the prefix given by `--pass-prefix`. Specific passphrase
length can be given using `--passphrase-length` and no symbols can
be activated with `--passphrase-no-symbols`. Second, a new private
and public keypair will be generated with the aforementioned passphrase
and with `ssh-keygen`'s `-t` and `-b` option given
respectively by `--ssh-t` and `--ssh-b`. Lastly, the public key
is written to stdout.

If the selected key exists, the public key is simply written to stdout.


## Options
* `-f`, `--fzf` Use fzf to select pass-name.
* `-r`, `--rofi` Use rofi to select pass-name.
* `-d`, `--ssh-dir` Directory holding ssh keyfiles, default $HOME/.ssh.
* `-p`, `--pass-prefix` Prefix under which passphrase are stored in pass, default sshkey-passphrase.
* `-n`, `--no-symbols` Do not use any non-alphanumeric characters.
* `-l <size>`, `--length=<size>` Provide a password length.
* `--ssh-t` ssh-keygen's -t option, the type of key to create.
* `--ssh-b` ssh-keygen's -b option, the number of bits in the key to create.
* `-h`, `--help` Show usage message.


## Installation


### ArchLinux

```sh
pacaur -S pass-ssh
```


### Other linuxes

```sh
git clone https://github.com/ibizaman/pass-ssh/
cd pass-ssh
sudo make install
```


### Requirements

* `pass 1.7.0` or greater.
* If you do not want to install this extension as system extension, you need to
enable user extension with `PASSWORD_STORE_ENABLE_EXTENSIONS=true pass`. You can
create an alias in `.bashrc`: `alias pass='PASSWORD_STORE_ENABLE_EXTENSIONS=true pass'`


## Contribution

Feedback, contributors, pull requests are all very welcome.


### Bump version

Update changelog and go to `aur/` and update `pkgver`. Then add a git
tag. Finally, run `make aur` and `make aur-push`.


## Acknowledgments

Thanks to [roddhjav](https://github.com/roddhjav) for creating
[pass-update](https://github.com/roddhjav/pass-update) from which this
script is heavily inspired.


## License

```
Copyright (C) 2017  Pierre PENNINCKX

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.
```

[build-img]: https://travis-ci.org/ibizaman/pass-ssh.svg?branch=master
[build-url]: https://travis-ci.org/ibizaman/pass-ssh
