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

## Generate Personal Access Token
We strongly recommend that you set up [two factor authentication (2FA)](https://github.com/settings/security) for your GitHub account - and any other accounts for that matter!
If you do, you will however need to take one more step when setting up CLI access.
**NB: From August 21st 2021, all users regardless of auth setup will require a PAT instead of password for CLI access**

- Generate new [Personal Access Token](https://github.com/settings/tokens) - _make sure to copy it!_
Use this instead of your password on prompt when making your first interaction with GitHub from the CLI (should only happen once)
If you are not being prompted for a password, run `git config --global --unset user.password` and try again!

## Install Chocolatey
_Note this is not really "essential" but will be very useful!_
[Chocolatey](https://chocolatey.org/) is a popular package manager for Windows applications.

To install it, we are going to use Command Prompt in an administrative shell.
_Note that once you have installed Chocolatey, you can go back to GitBash and interact with it there._

**- Open Command Prompt in an administrative shell**
  - Open the Start menu
  - Type "command" - Command Prompt should come up as the Best Match result
  - Right click on Command Prompt and click 'Run as administrator'
  - You may be asked for permission to continue, if so, click "Yes"!
**- Check your Execution Policy**
  - In your admin shell, run `Get-ExecutionPolicy`
  - If it returns Restricted or Undefined run: `Set-ExecutionPolicy Unrestricted`
**- Install Chocolatey**
  - In your admin shell, run `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`
  - It may take a minute for the command to complete
  - If no errors come up, you should be good to go!
**- Confirm your Chocolatey installation**
  **- Close your admin shell and return to GitBash**
  - In GitBash, run `choco --help` and you should be greeting with a help menu
_Note that to upgrade Chocolatey (recommended before you install anything via Chocolately) run: choco upgrade chocolatey_

## Get node locally and install a global package
Although Docker can be used for many things, we will also install node locally for some global use tools that we may use.

**- Download and install nodejs using the [official installers](https://nodejs.org/en/download/package-manager)**
  - When going through the install wizard, the standard options are all okay for our usage
  - Check the box to allow automatic installation of additional tools
  - Select 'yes' when asked if you want to let node make changes to your device
  - After the installation, lookout for the Powershell window prompting to install the additional tools and press any key to continue
  - Again, select 'yes' when asked if you want to let Powershell make changes to your device
  - Get a cup of tea, this part can take a few minutes as it installs a bunch of other good things!
  - Once the scripts have finished running, follow the prompt to hit ENTER and restart your machine
**- Confirm your node installation**
  - After restarting your machine, open GitBash and type `node -v`
  - If you see a version number eg. `v18.16.1` then your install was successful!
  - You should also get version numbers back for `npm -v` and `npx -v`
  - If this does not work try winpty `node -v`
  - If winpty worked then follow the [instructions below]https://github.com/getfutureproof/fp_guides_wiki/wiki/Windows-Setup#the-bashrc-file) to add an alias to a `.bashrc` file
**- Install your first global node package**
  - `npm install -g laughs`
  - `ha` - wait for a joke!

## Get python locally and discover the Zen of Python
To have control of our Python versions we are going to use a tool called `pyenv`. `pyenv` allows us to easily switch between different Python versions which can be very helpful when working on different projects and with other people.

**- Download and install pyenv with Chocolately**
  - In GitBash, run choco install pyenv-win
  - Restart your bash shell and run pyenv --version to confirm the installation
    - If you receive a permission denied or a command not found error, check the [documentation](https://github.com/pyenv-win/pyenv-win#finish-the-installation) for how to manually set environment variables even if you used [Chocolatey](https://chocolatey.org/).
  - Navigate to your home directory with `cd ~` and run `pyenv rehash`
**- Install Python 3.11.5 with pyenv and set it as your global default version**
  - At time of writing 3.11.5 is the latest stable version
  - `pyenv install 3.11.5` (we can easily get other versions later on if you want)
  - `pyenv global 3.11.5`
  - `pyenv rehash`
**- Confirm your python installation**
  - `python --version`
  - If you see a version number eg. `Python 3.11.5` then your install was successful!
  - You should also get a version number back for `python -m pip --version`
    - **If this does not work** try `winpty python --version`
    - **If winpty worked** then follow the [instructions below](https://github.com/getfutureproof/fp_guides_wiki/wiki/Windows-Setup#the-bashrc-file) to add an alias to a `.bashrc` file
  - **If you are still having trouble, see the [Troubleshooting](https://github.com/getfutureproof/fp_guides_wiki/wiki/Windows-Setup#Troubleshooting) guide below** _- this is more likely if you already have Python installed and/or are running Windows 10 1905 or newer_
**- Check out the 'Zen of Python'**
  - `python` - to enter a python shell (bye, bash!)
  - `import this` - this will show you the Zen of Python!
  - `exit()` - to exit the python shell

## Install Docker
Download [Docker Desktop](https://www.docker.com/products/docker-desktop/)
Test your install from the command line by running `docker run hello-world`

## The .bashrc file
A `.bashrc` file is a configuration file for the bash shell - which you'll be using if running GitBash. The dot at the beginning means it is a hidden file!

**To access the file**
- In GitBash, run `cd ~` which will take you to your home directory
- Run `ls -lah` to see all the files (even hidden ones) in the directory
- Look for one called `.bashrc`
  - If it does not exist, create it with `touch .bashrc`
- Open it in a text editor of your choice

**To add an alias**
If you find yourself typing something lengthy a lot, you can create an 'alias'. For example, if you have to run `winpty python` everytime you want to run a python shell, you might wish that you could just use `python`.

The anatomy of an alias definition is : `alias <what-i-want-to-use>='<the-actual-command>'`
- eg. `alias node='winpty node'` (genuinely useful)
- eg. `alias npm='winpty npm'` (genuinely useful)
- eg. `alias python='winpty python'` (genuinely useful)
- eg. `alias pip='winpty pip'` (genuinely useful)
- eg. `alias showstuff='ls'` (genuinely not useful)

**After making changes**
Make sure you save the file and reload GitBash before trying out your shiny new aliases - or any other changes/additions you may make in this file!
- Either close and reopen GitBash
- Or run `source ~/.bashrc`

## Troubleshooting
### Issues installing Python via `pyenv`
- If you are running Windows 10 1905 or newer, you made need to disable the built-in Python launcher via Start > "Manage App Execution Aliases" and disabling the "App Installer" aliases for Python.
- Failing that you may have to alter your [environment variables](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/) so that any `pyenv` paths are higher in the list, and therefore take precedence over any other Python paths, including other Python package managers such as Anaconda. _(Remember to restart your machine for changes to take effect.)_
- As a last resort you might have to [uninstall Python](https://www.architectryan.com/2018/03/17/add-to-the-path-on-windows-10/) before pyenv will work.
