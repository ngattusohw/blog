# The Ultimate Mac Setup Guide for New Developers

So you've got a shiny new Mac and you're ready to start coding? Congratulations! Setting up your development environment properly from the beginning will save you countless hours of frustration later. This guide will walk you through installing essential tools that will supercharge your development workflow.

## 1. Install Homebrew

Homebrew is the missing package manager for macOS and the foundation of any good development setup. It allows you to easily install and manage software that Apple doesn't include by default.

Open Terminal and run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the prompts, and when installation is complete, make sure to follow any instructions about adding Homebrew to your PATH.

After installation, run:

```bash
brew doctor
```

This will check for any potential issues with your Homebrew installation.

You might see an error that looks like this:

```
Warning: Homebrew's bin was not found in your PATH.
```

In this case, follow the instructions in the prompt and run the commands:

```bash
# Append to the .zprofile file:
echo >> ~/.zprofile
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile

# Evaluate the Homebrew shell environment:
eval "$(/opt/homebrew/bin/brew shellenv)"
```

If you see "Your system is ready to brew." – you're in the clear!

## 2. Install and Configure zsh

macOS has used zsh as the default shell since Catalina, so you likely already have it installed. To confirm, run:

```bash
zsh --version
```

If for some reason you need to install it:

```bash
brew install zsh
```

To make zsh your default shell (if it isn't already):

```bash
chsh -s $(which zsh)
```

## 3. Install Oh My Zsh

Oh My Zsh is a framework for managing your zsh configuration. It comes with helpful plugins, themes, and functions that will make your terminal experience more productive and enjoyable.

Install it by running:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

### Customizing Oh My Zsh

After installing Oh My Zsh, you can customize it by editing your `~/.zshrc` file:

```bash
nano ~/.zshrc
```

Some popular customizations include:

- **Changing the theme**: Find the line `ZSH_THEME="robbyrussell"` and change it to another theme like `agnoster`, `powerlevel10k`, or any from the [themes gallery](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes).
- **Adding plugins**: Find the line starting with `plugins=(git)` and add more plugins, like:

```bash
plugins=(git vscode brew node npm python docker)
```

After making changes, apply them with:

```bash
source ~/.zshrc
```

## 4. Install Raycast

Raycast is a productivity tool that replaces your Mac's Spotlight with a more powerful alternative. It helps you get things done faster with quick commands, extensions, and integrations.

Install it using Homebrew:

```bash
brew install --cask raycast
```

After installation, launch Raycast and go through the initial setup. Some developer-friendly extensions to consider adding:

- GitHub
- Terminal
- Clipboard History
- Color Picker
- Window Management

## 5. Install SuperWhisper

SuperWhisper is a tool that offers high-quality transcription capabilities for developers who work with audio or want to transcribe meetings.

Install it using Homebrew:

```bash
brew install --cask superwhisper
```

After installation, launch SuperWhisper and follow the setup instructions:

1. Allow necessary permissions
2. Configure your preferred settings for transcription
3. Set up keyboard shortcuts if desired

## 6. Install Cursor

Cursor is an IDE built on VSCode that integrates AI capabilities to help you code faster.

Install it using Homebrew:

```bash
brew install --cask cursor
```

After installation, launch Cursor and:

1. Sign in with your account or create a new one
2. Install any extensions you need for your development workflow
3. Configure settings according to your preferences
4. Set up AI features if you want to use them

## Additional Developer Tools Worth Installing

Now that you have the essentials, consider adding these other tools:

### Command Line Tools

```bash
# Git (version control)
brew install git

# NVM (Node Version Manager)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# Node.js using NVM
nvm install --lts

# Yarn package manager
npm install -g yarn

# Python
brew install python

# Visual Studio Code (alternative to Cursor)
brew install --cask visual-studio-code
```

After installing NVM, add these lines to your ~/.zshrc file if they aren't added automatically:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
```

Then reload your terminal configuration:

```bash
source ~/.zshrc
```

To verify your installations:

```bash
# Check NVM version
nvm --version

# Check Node.js version
node --version

# Check Yarn version
yarn --version
```

### Development Apps

```bash
# Docker (containerization)
brew install --cask docker

# Postman (API testing)
brew install --cask postman

# iTerm2 (better terminal)
brew install --cask iterm2

# Rectangle (window management)
brew install --cask rectangle
```

## Setting Up SSH for GitHub

Using SSH keys allows you to connect to GitHub without having to enter your username and password each time. Here's a detailed guide on setting up SSH for GitHub on your Mac:

### 1. Check for Existing SSH Keys

First, check if you already have SSH keys on your machine:

```bash
ls -al ~/.ssh
```

If you see files named `id_ed25519.pub`, `id_rsa.pub`, or similar, you already have SSH keys. If not, you'll need to create them.

### 2. Generate a New SSH Key

To create a new SSH key with enhanced security, run:

```bash
# For newer systems, Ed25519 is recommended
ssh-keygen -t ed25519 -C "your_email@example.com"

# Or use RSA with 4096 bits for broader compatibility
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

When prompted to "Enter a file in which to save the key," press Enter to accept the default location.

Next, you'll be asked to enter a passphrase. While you can leave it empty, adding a passphrase provides an extra layer of security.

### 3. Add Your SSH Key to the ssh-agent

Start the ssh-agent in the background:

```bash
eval "$(ssh-agent -s)"
```

Add your private key to the ssh-agent:

```bash
# For macOS Monterey (12.0) or later
ssh-add --apple-use-keychain ~/.ssh/id_ed25519

# For older macOS versions
ssh-add -K ~/.ssh/id_ed25519

# If you used RSA instead
ssh-add --apple-use-keychain ~/.ssh/id_rsa  # Or -K for older macOS
```

### 4. Add Your SSH Key to GitHub

Copy your public key to the clipboard:

```bash
# For Ed25519 keys
pbcopy < ~/.ssh/id_ed25519.pub

# For RSA keys
pbcopy < ~/.ssh/id_rsa.pub
```

Now, add the key to your GitHub account:

1. Go to GitHub and sign in
2. Click your profile photo in the top right, then click **Settings**
3. In the left sidebar, click **SSH and GPG keys**
4. Click **New SSH key**
5. Add a descriptive title (e.g., "MacBook Pro Work")
6. Paste your key into the "Key" field
7. Click **Add SSH key**

### 5. Test Your Connection

Test that your SSH connection to GitHub is working:

```bash
ssh -T git@github.com
```

You might see a warning about authenticating the host. Type `yes` to continue.

If successful, you'll see a message like:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### 6. Configure Git to Use SSH

For new repositories, when you clone, use the SSH URL instead of HTTPS:

```bash
# Instead of https://github.com/username/repo.git
git clone git@github.com:username/repo.git
```

For existing repositories that use HTTPS, change the remote URL:

```bash
# Check current remote URL
git remote -v

# Change from HTTPS to SSH
git remote set-url origin git@github.com:username/repo.git
```

Now you can push and pull without entering your username and password each time!

## Setting Up Your Development Workspace

### Create a Development Folder and Add It to Finder Favorites

First, let's create a dedicated folder for all your development projects:

```bash
mkdir -p ~/Developer
```

Now, let's add this folder to your Finder favorites for quick access:

1. Open Finder
2. Press Cmd+Shift+G and type `~/Developer`, then click "Go"
3. With the Developer folder open, press Cmd+Shift+T (or drag the folder to the sidebar)

This will add your Developer folder to the Favorites section in Finder's sidebar, making it easily accessible whenever you need it.

You can also do this from Terminal if you prefer:

```bash
# Make sure the folder exists
mkdir -p ~/Developer

# Add to Finder favorites (requires additional setup)
mysides add Developer file:///Users/$USER/Developer
```

Note: The `mysides` command requires installation: `brew install mysides`

## Final Touches

### Create a GitHub SSH Key

Generate an SSH key for GitHub:

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Add it to your SSH agent:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Copy the key and add it to your GitHub account:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

### Set Up Global Git Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

## Conclusion

Congratulations! You've set up your Mac with essential developer tools that will boost your productivity. This setup gives you a solid foundation with:

- Homebrew for package management
- zsh and Oh My Zsh for a powerful terminal experience
- Raycast for quick actions and productivity
- SuperWhisper for transcription needs
- Cursor for AI-enhanced coding

Remember that your development environment will evolve as you grow as a developer. Don't be afraid to customize it further based on your specific needs and preferences.

Happy coding!

