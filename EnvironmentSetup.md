# Dev environemnt setup

This file is an explanation on how to setup the development environment for PC subteam projects.

I recommend that you write all the commands by hand instead of copying them directly from this file.

## Prerequisites:
- Basic use of a terminal with: `cd`, `ls`, `mkdir`, `pwd`, `echo`, `rmdir`, `touch`, `rm`. 
  - After you followed the `sudo mandb` section in the Operating System setup, Use `whatis` and `man` to learn what these commands do 
  

## Terms 
 - shell: the (usually) textual interface to the operating system, i.e. CMD, bash, PowerShell, ash, fish, zsh...
 - terminal: the application / window in which some shell runs.
 - Windows shell instances: (powershell/cmd) doesn't really matter which one, unless specified otherwise explicitly.
 - WSL: a feature of Windows that allows developers to run a Linux environment without the need for a separate virtual machine
 - Fedora Remix: a linux distribution
 - bash: the default shell fedora uses (equivalent to cmd/powershell on windows)


## Operating System setup
 - Download Vscode by running `winget install -e --id Microsoft.VisualStudioCode` in a windows shell instance
 - Download the extension for vscode named WSL by pressing Ctrl+p, pasting this `ext install ms-vscode-remote.remote-wsl` and pressing enter
 - Ensure you have Windows Terminal installed by running `winget install microsoft.windowsterminal` in a windows shell instance
 - Run a windows shell instance as administrator (Right click should show a Run as administrator option) 
 - Install wsl with `wsl --install`
 - Download newest Fedora Remix WSL release by pressing the .msixbundle file in the Assets [here](https://github.com/WhitewaterFoundry/Fedora-Remix-for-WSL/releases)
 - Once the file is downloaded run the file and let the installer run
 - In the new **fedora** shell that opened enter your user name and password for the fedora account make the password memorable because you will write it alot
 - In a **fedora** shell change the wsl config by running the command below. After that enter your password. Every command that uses `sudo` will request a password, `sudo` means you want to run the command with elevated permissions. **when writing the password the letters aren't shown**
   - `printf '[interop]\nappendWindowsPath = false' | sudo tee -a /etc/wsl.conf` (This appends the string to a file that needs elevated permissions to be written to)
 - Close all fedora terminal windows 
 - In a windows shell instance restart fedoraremix with the new configuration by running `wslconfig /t fedoraremix`
 - In a new fedora terminal (Use windows terminal to open a new terminal) update everything on your system with `sudo dnf upgrade -y` 
   - `sudo` because this command needs elevated permission. 
   - `dnf` is the package manager, it helps you install, find and in this case `upgrade` packages on your system (of course it does alot of other things). 
   - The `-y` flag means we want to accept everything installed without `dnf` asking to accept
 - Update your `man` and `whatis` entries by running the command: `sudo mandb`
 - Make sure fedoraremix is your default wsl distrobutions by running `wsl --set-default fedoraremix` in a **windows** shell instance
 - Make sure you are using WSL2 by running `wsl -l -v` (`-l`: list, `-v`: verbose) in a **windows** shell instance and make sure the vesion of `fedoraremix` is 2
 - You have finished downloading the Operating System!
 - From now on we will be working almost only with fedora. This means that when you search for instructions on how to do things you search for **Fedora** instructions not Windows instructions.


## Git setup
 - Install git in Fedora with this command: `sudo dnf install git -y`
 - SSH setup:
   - Generate an ssh key by running `ssh-keygen`. Unless you *want* to change the default location or use a passphrase, just press enter and use the defaults.
   - Copy the public key by copying the complete output of this command `cat ~/.ssh/id_rsa.pub`
   - Paste the public key into GitHub > Settings > SSH and GPG keys > New SSH key > key. (You don't need to set a title or a key type).
   - If you want to generate the key in a different path, use a passphrase to protect it or any other optional features you can [`man ssh-keygen`](https://www.man7.org/linux/man-pages/man1/ssh-keygen.1.html) or [`curl cheat.sh/ssh-keygen`](https://cheat.sh/ssh-keygen).
## Flutter setup
 - Download flutter by cloning the git repository into a path of your choice by running: `git clone --branch stable --single-branch --filter=blob:none git@github.com:flutter/flutter` 
  - This is probably your first clone, so ssh will prompt you about a new host you should enter `yes` because github.com is a trusted host
 - Add flutter to `$PATH` by running: `echo 'export PATH="${PATH}:'"${PWD}/flutter/bin\"" >> ~/.bashrc` and then run `. ~/.bashrc` 
    - `echo`: Prints a given string to the terminal (stdout)
    - `>>`: Redirects the output (stdout) of a specfic command to a somewhere else in this case a file (`~/.bashrc`)
    - `.bashrc`: a bash script that is run everytime a bash shell starts
    - `. ~/.bashrc`: Reruns the `.bashrc` file (we need to de this because changes where made to the file)
    - `~`: a shrortcut for /home/your_username/
 - Check your installation by running: `flutter doctor` and ensure you see this: [✓] Flutter (Channel stable, .....)
 - You have officially Downloaded Flutter!

## Flutter native linux app setup
 - Install needed packages for linux development by running: `sudo dnf install clang cmake ninja-build gtk3-devel -y`
 - Run `flutter doctor` again, now this should be written: [✓] Linux toolchain - develop for Linux desktop

## Flutter web app setup
 - Install chromium: `sudo dnf install chromium -y`
 - Add this to your `.bashrc` file: `export CHROME_EXECUTABLE=$(which chromium-browser)` (Look at Flutter setup for refresher)
 - Run: `flutter doctor` and you should see this: [✓] Chrome - develop for the web

