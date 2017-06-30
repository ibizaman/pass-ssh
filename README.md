# pass ssh 0.1 [![build status][build-img]][build-url]

A [pass](https://www.passwordstore.org/) extension that lets you quickly
create ssh keypairs and output public keys using
[fzf](https://github.com/junegunn/fzf) or
[rofi](https://davedavenport.github.io/rofi/).


## Usage

```
pass ssh [--help,-h]
    [--fzf,-f]|[--rofi,-r] [--ssh-dir <s>,-d <s>]
    [--pass-prefix <s>,-p <s>] [--passphrase-no-symbols,-n] [--passphrase-length <s>,-l <s>]
    [--ssh-t <s>] [--ssh-b <s>]
```

`pass-ssh` provides an interactive solution to create ssh private
and public keypairs with passphrases stored in `pass` as well as
write the public key to stdout. It will show all available ssh keys in
either `fzf` or `rofi`, wait for the user to select one and
write the public key to stdout.

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


## Examples

Combined with a clipboard manager like [`xclip`](https://github.com/astrand/xclip):
```
pass ssh | xclip -in -selection clipboard
```


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
