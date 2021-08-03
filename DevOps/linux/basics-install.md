# Basics Install

- [X] Git
- [x] VSCode
- [X] Node.js
- [X] Python (3.7)
- [X] Google Chrome
- [X] ZSH (Oh My Zsh)


## VSCode
Installed via ubuntu software program

## Chrome

1) prompt terminal:

<kbd>Alt</kbd>+<kbd>Ctrl</kbd>+<kbd>t</kbd>

2) use wget to download latest `.deb` package:
   ```bash
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   ```
3) install package as super user:
   ```bash
   sudo apt install ./google-chrome-stable_current_amd64.deb
   ```

## Git / Github

1) install git 
   ```bash 
   sudo apt install git
   ```
2) set name & email
   ```bash 
   git config --global user.email "my_email@email.com"
   git config --global user.name "Me"
   ```
3) generate SSH key
   ```bash 
   ssh-keygen
   ```

4) copy contents of ~/.shh/id_rsa.pub into GitHub account (Settings > SSH Keys > New SSH Key)
5) use SSH option to git clone your repos & should be all set to pull/push

## Node

1) install nodejs 
   ```bash 
   sudo apt install nodejs
   ```

2) install npm 
   ```bash 
   sudo apt install npm
   ```
3) install yarn
   ```bash
   npm install --global yarn
   ```

5) install nvm & install node version
   ```bash
   wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
   nvm install 16.6.1
   nvm use 16
   node --version
   ```

## cURL 
1) install curl
   ```bash
   sudo apt install curl
   ```

## ZSH 

1) install zsh 
   ```bash 
   sudo apt install zsh
   ```

2) find location
   ```bash
   which zsh
   ```

3) make default shell
   ```bash
   chsh -s /usr/bin/zsh
   ```
   or just:
   ```bash
   chsh -s $(which zsh)
   ```

NOTE: need to logout / login to make change. I selected the 0 option when prompted on fist launch (no zsh config file).

4) should be clear but can check which shell is running
   ```bash
   echo $SHELL
   ```

5) install Oh-my-zsh
   ```bash
   sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
   ```

## Python 3.7

1) update packages list & install prerequisites
   ```bash
   sudo apt update
   sudo apt install software-properties-common
   ```

2) add deadsnakes PPA to sources list
   ```bash
   sudo add-apt-repository ppa:deadsnakes/ppa
   ```

3) Once repo is enabled, install Python 3.7
   ```bash
   sudo apt install python3.7
   ```

If/When you want to install Postman, see: 
https://medium.com/@chaudharypulkit93/installing-postman-on-ubuntu-the-right-way-3bed244b7e51







