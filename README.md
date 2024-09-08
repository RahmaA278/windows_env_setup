# Windows Environment Setup
## VS Code
VS Code is a popular code editor for building and debugging your applications. Download and install [VS Code](https://code.visualstudio.com/download).
## Git & GitBash Setup
Git is a version control system that lets developers track source code changes during software development. Git Bash is an application for Microsoft Windows, allowing developers to use Git in a command-line interface. Install the latest release of git. Keep the standard options (make sure Git Bash is included in your install). When selecting the various options:
- your default editor: Visual Studio Code
- PATH environment: 'Git from the command line and also from 3rd-party software'
- HTTPS transport backend: OpenSSL library
- line ending conversions: 'checkout as-is, commit Unix-style line endings'
- git pull: default
- credential helper: Git Credential Manager Core
- enable symbolic links: true Others are up to you but the defaults are generally good.

Open GitBash and configure git:
`git config --global user.name "your name"` eg. `git config --global user.name "lafosse"`
`git config --global user.email "your email"` eg. `git config --global user.email "admin@lafosse.com"`

When working on different operating systems, our line endings may end up getting changed. We will unify our line ending to match Unix-style:
`git config --global core.autocrlf input`

## Set up your SSH key
- In your terminal run `ssh-keygen` and follow the instructions. If it asks if you want to overwrite, say no.
- In your terminal run `cat ~/.ssh/id_rsa.pub` and copy the output. If it returns with an error with cat open up your Windows PowerShell and continue the steps here.
- Visit the [GitHub SSH Keys setting page](https://github.com/settings/keys) in your browser and click 'New SSH Key'
- Give it a title, anything you like to indicate the machine this key is for, and paste in your key
- The first time you clone and push you may see warning that a new RSA key is being added, this is normal!

**_NB: If using the VS Code terminal, we recommend selecting Git Bash as your Default Shell:_**

- Open a new terminal in VS Code (see the application top bar)
- From the dropdown that likely says 1. Powershell, choose 'Select Default Shell' and select Git Bash
- Close the terminal and open a new one - the dropdown should now say '1. bash'
