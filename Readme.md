&hearts; the Vim.

## Fresh install

**Warning this will blow away any vim/bash setups you have currently. You may
want to back up existing files.**

- Xcode should be installed on your system from the App Store
- Install Xcode command line tools by running `xcode-select --install` in a terminal window
- Install Homebrew if you don't already by running `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` in a terminal window
- Make sure you have git installed by running `brew install git` in a terminal window
- Make sure you have ripgrep installed by running `brew install ripgrep` in a terminal window
- In a terminal window cd to the dotfiles directory and run `bin/install world`
- A helpful way to reload the terminal once the dotfiles are installed and terminal has been relaunched is to run our alias `reload` in a terminal window (this only effects reloading of the current window not all terminal windows)
- Set reasonable [OSX defaults][osxdefaults]
- [asdf][asdf] extendable version manager
  - Ruby: `asdf plugin-add ruby && asdf install ruby | cat .ruby-version`
  - Might want to create a `~/.tool-versions` file with base versions set. Project level `.tool-versions` files will override the defaults.
  - You can use legacy files for versions (.ruby-version) by setting `legacy_version_file = yes` in a `~/.asdfrc` config file.

## Settings

### Rock a sweet Bash setup

The Bash setup is fairly bare bones out of the box. To override or add
any additional settings create a `~/.bashrc.local` file and add
any customization.

The default Bash settings support the [asdf][asdf] environment.

### Git credentials

To setup your git credentials correctly you'll need to add a `.gitconfig.local`
file to your `$HOME` directory and add the following:

```
[user]
  name = YOUR_GIT_AUTHOR_NAME
  email = YOUR_GIT_AUTHOR_EMAIL
[github]
  user = YOUR_GITHUB_USERNAME
```

### Override Vim settings

To override or add any additional settings create a `~/.vimrc.local` file and
add any customization.

Vim is setup with [vim-plug][vim-plug] as it's plugin manager. The default
plugins are enabled within the [.vimrc][vimrc] file. To load localized plugins
add them to a `~/.vimrc.bundles` file.

To install the plugins open up vim by running `vim` in a terminal window and
then typing `:PlugInstall`. If you get an error while opening up vim about not
being able to find `colorscheme pigment` that's ok as the `:PlugInstall` will
fix this for the next time you launch vim.

## Tips

### GPG (Optional)

First you will need to generate a GPG key and add it to your github settings
from [here](https://help.github.com/articles/generating-a-new-gpg-key/). Will
also require you to install gnupg via homebrew `brew install gnupg`.

You will need to install GPG Keychain for GPG signing to happen automatically.
See [GPG Tools](https://gpgtools.org/) for more information. There are ways to
do this through homebrew, but the setup is a bit much. To obtain your GPG
signing key you can either open up GPG Keychain, or run `gpg --list-keys` and
add this to the `GIT_SIGNING_KEY` in your `.bashrc.local` file.

You will also need to make your GPG signing key the primary one. You can do this
by opening up GPG Keychain and doing these steps:

- select your key
- hit the details button
- select User IDs from the menu
- right click on your user id and select primary
- select 'save to keychain' when the dialog pops up
- and add this to your .gitconfig.local:

```
[user]
  signingKey = YOUR_GIT_SIGNING_KEY
[commit]
  gpgsign = true
[gpg]
  program = /usr/local/bin/gpg
```

### GPG (Without GPG Tools)

- `brew install gnupg gpg-agent pinentry-mac`
- add `pinentry-program /usr/local/bin/pinentry-mac` in ~/.gnupg/gpg-agent.conf
- add the git config from above

### Install Polarized terminal themes

Included in the vimrc is `Plug mkitt/pigment`. This is the color settings for
Vim. Any color profile should work with this theme including the defaults from
Apple. Included from the [pigment][pigment] repository is the Polarized light
and dark profiles. Import these profiles into Apple's Terminal.app and set one
as the default. They should be found in:

```
~/.vim/plugged/pigment/profiles/
```

### Turn caps lock into the control key

The control key is in an awkward position and the caps lock key is
basically useless. It's right there in the home row, so you might as
well put it to good use.

1.  Open up System Preferences

- Select `Keyboard`
- Select `Modifier Keys`
- From the drop down, select `^ Control` under the `Caps Lock` setting
- In the `Select Keyboard` drop down, set it for both internal and external keyboards

### Mouse support for Terminal

To get full mouse support (scrolling, clicking, etc...) within Terminal
Vim, install the [SIMBL][simbl] [MouseTerm][mouseterm] plug-in.

<!-- Markdown links -->

[asdf]: https://github.com/asdf-vm/asdf
[mouseterm]: https://bitheap.org/mouseterm/
[osxdefaults]: http://mths.be/osx
[simbl]: http://www.culater.net/software/SIMBL/SIMBL.php
[vim-plug]: https://github.com/junegunn/vim-plug
[pigment]: https://github.com/mkitt/pigment
[vimrc]: /dots/vimrc
