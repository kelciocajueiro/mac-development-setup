# Set up an Apple Mac for Software Development [2023]

## System Preferences

### Appearance

Show scroll bars → Always

### Dock

Remove workspace auto-switching by running the following command:

```bash
defaults write com.apple.dock workspaces-auto-swoosh -bool NO
killall Dock
```

Remove all unnecessary apps from the dock, ensuring that only the most frequently used applications were present

Disable `Show recent applications in Dock`

### Siri & Spotlight

Disable `Ask Siri`

Uncheck useless categories for Search Results

### Finder Settings

General → New Finder windows show → Home folder

General → Show these items on the desktop → None

Sidebar → Add Home and your Code directory and uncheck the unnecessary boxes

Advanced → Show all filename extensions → Yes

Advanced → Show warning before changing an extension → No

Advanced → When performing a search → Search the current folder

```bash
# take screenshots as jpg (usually smaller size) and not png
defaults write com.apple.screencapture type jpg

# do not open previous previewed files (e.g. PDFs) when opening a new one
defaults write com.apple.Preview ApplePersistenceIgnoreState YES

# show Library folder
chflags nohidden ~/Library

# show hidden files
defaults write com.apple.finder AppleShowAllFiles YES

# show path bar
defaults write com.apple.finder ShowPathbar -bool true

# show status bar
defaults write com.apple.finder ShowStatusBar -bool true

killall Finder;
```

### Keyboard

Set the key repeat rate to the fastest setting and minimize the delay until repeat, ensuring the typing speed is not hindered by a slow repeat rate

### User Defaults

Change the default folder for screenshots:

```bash
defaults write com.apple.screencapture location /Users/kelciobarreto/Pictures/
killall SystemUIServer
```

### Security & Privacy

Network → Active Firewall

# Homebrew

Homebrew provides a package management system for macOS, enabling you to quickly install and update the tools and libraries that you need

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

You should also amend your PATH, so that the versions of tools that are installed with Homebrew take precedence over others. To do this, edit the file *.zshrc* (after installing zsh) in your home directory to include this line:

```bash
export PATH="/usr/local/bin:/usr/local/sbin:~/bin:$PATH"
```

To check that Homebrew is installed correctly, run this command in a terminal window: `brew doctor`

To update the index of available packages, run this command in a terminal window: `brew update`

# Git

To install, run `brew install git`

When done, to test that it installed properly you can run `git —-version`

Update your git settings

```bash
git config --global user.name "John Doe"
git config --global user.email "you@domain.com"
```

They will get added to your `.gitconfig` file

To prevent `git` from asking for your username and password every time you push a commit you can cache your credentials by running the following command

```bash
git config --global credential.helper osxkeychain
```

Change globally default branch name from `master` to `main`

```bash
git config --global init.defaultBranch main
```

Print global git configuration

```bash
git config --list
```

Follow this link to get more information about Git and GitHub configuration: [Git · macOS Setup Guide](https://sourabhbajaj.com/mac-setup/Git/)

# Vim

Vim is a highly configurable text editor built to make creating and changing any kind of text very efficient. It is included as "vi" with most UNIX systems and with Apple macOS

To install the latest version, use homebrew: `brew install vim`

### The Ultimate vimrc

This is a collection of vimrc configurations to make easy the usage of vim.

Download the vimrc files: `git clone https://github.com/amix/vimrc.git ~/.vim_runtime`

To install the complete version, run: `sh ~/.vim_runtime/install_awesome_vimrc.sh`

To update the vimrc scripts, run: `cd ~/.vim_runtime && git pull --rebase && cd -`

How to install IBM Plex on macOS

```bash
brew tap homebrew/cask-fonts
brew install font-ibm-plex --cask
```

# Zsh

Zsh is a Unix shell that is built on top of bash (the default shell for macOS) with additional features. It's recommended to use zsh over bash. It's also highly recommended to install a framework with zsh as it makes dealing with configuration, plugins and themes a lot nicer

Install zsh using Homebrew: `brew install zsh`

## Oh My Zsh

Oh My Zsh is a framework for managing your Zsh configuration. Install it via the command-line:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

The installation script should set `zsh` to your default shell, but if it doesn't you can do it manually: `chsh -s $(which zsh)`

### Plugins

****zsh-syntax-highlighting****

The Syntax Highlighting plugin adds beautiful colors to the commands you are typing

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

****zsh-autosuggestions****

This plugin auto suggests any of the previous commands. Pretty handy! To select the completion, simply press → key

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

To update everything in Oh My Zsh to recent version, run this command in a terminal window: `omz update`

To apply the changes you make you need to either **start new shell instance** or run: ****`source ~/.zshrc`

# iTerm 2

iTerm2 is an open source replacement for Apple's Terminal. It's highly customizable and comes with a lot of useful features.

```bash
brew install --cask iterm2
```

### Useful ****tools****

**Fzf**: General-purposed command-line fuzzy finder: `brew install fzf`

**Wget**: Internet file retriever (like curl): `brew install wget`

**Tree**: Displays directories as trees: `brew install tree`

**Jq**: Lightweight and flexible command-line JSON processor: `brew install jq`

**Neofetch**: Fast, highly customizable system info script: `brew install neofetch`

**Lolcat**: Rainbows and unicorns in your console: `brew install lolcat`

### ****Quick Look plugins****

There are some quicklook plugins that makes it really easy to preview files in Finder

```bash
brew install --cask \
    qlcolorcode \
    qlstephen \
    qlmarkdown \
    quicklook-json \
    qlprettypatch \
    quicklook-csv \
    qlimagesize \
    betterzip \
    webpquicklook \
    quicklookase \
    qlvideo \
    suspicious-package
```

# Eclipse Temurin

The Eclipse Temurin project provides code and processes that support the building of runtime binaries and associated technologies that are high performance, enterprise-caliber, cross-platform, open-source licensed, and Java SE TCK-tested for general use across the Java ecosystem

By default, it would install the latest version:

```bash
brew install --cask temurin
```

You can also add the following function at the top of your *~/.bashrc* or *~/.zshrc* to easily switch the different JDK versions should you choose to install all the different versions

```bash
jdk() {
    version=$1
    export JAVA_HOME=$(/usr/libexec/java_home -v"$version");
    java -version
}
```

You need to set a default `JAVA_HOME` in the *~/.zshrc* and bind it to the `$PATH`

# Apache Maven

Apache Maven is a widely used build automation and project management tool for Java-based software projects. It provides a comprehensive framework and set of conventions to streamline the building, packaging, and deployment of applications.

To install, run the command: `brew install maven`

You might need to set a default `MVN_HOME` in the *~/.zshrc* and bind it to the `$PATH`

### Protocol Issue

Visit `http://repo.maven.apache.org/`

If it says https required, you need to add this chunk of code to your `settings.xml` inside `<mirrors>`

```
<mirror>
  <id>central-secure</id>
  <url>https://repo.maven.apache.org/maven2</url>
  <mirrorOf>central</mirrorOf>
</mirror>
```


# Docker

# OS Productivity

**Rectangle**: Move and resize windows in macOS using keyboard shortcuts or snap areas: `brew install rectangle`

**AltTab**: Brings the power of Windows’s ‘alt-tab’ window switcher to macOS: `brew install --cask alt-tab`

**KeepingYouAwake** - Prevents your Mac from going to sleep: `brew install --cask keepingyouawake`

**App Cleaner** - When removing an app, will search your file system for related files that should be removed as well: `brew install --cask app-cleaner`

**Kap** - Open-source screen recorder built with web technology: `brew install --cask kap`

**Stats** - See network traffic, CPU temperature and RAM usage at a glance: `brew install stats`

**Itsycal** - Have a calendar in the menu bar: `brew install itsycal`

# Other Apps

**IntelliJ IDEA** - Java IDE: `brew install --cask intellij-idea`

**Visual Studio Code** - Microsoft IDE: `brew install --cask visual-studio-code`

**Spotify** - Music streaming service: `brew install --cask spotify`

**VLC Player** - Multimedia player: `brew install --cask vlc`

# References

[Introduction · macOS Setup Guide](https://sourabhbajaj.com/mac-setup/)

[How to Set up an Apple Mac for Software Development](https://www.stuartellis.name/articles/mac-setup/)

[Mac Setup for Web Development [2023]](https://www.robinwieruch.de/mac-setup-web-development/)

[Setting up a Mac for Development](https://dev.to/w3cj/setting-up-a-mac-for-development-3g4c)

[Mac setup for web development 2023 | Nikolas Barwicki](https://nikolasbarwicki.com/articles/mac-setup-for-web-development-2023)

[macOS set up for coding and development (2023 edition)](https://www.atpeaz.com/macos-set-up-for-coding-and-development/)
