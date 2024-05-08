<div align="center">
    <h1 align="center">Environment Configuration Ubuntu WSL</h1>
</div>

## Getting Started

This is the configuration guide of my working environment Ubuntu WSL.

### Prerequisites

You must have [Windows Terminal](https://www.microsoft.com/store/productId/9N0DX20HK701?ocid=pdpshare) installed and you must also have the latest version of [Powershell](https://www.microsoft.com/store/productId/9MZ1SNWT0N5D?ocid=pdpshare) installed.

### Installation

The next step is to install WSL by executing the following command in Powershell Terminal:

```sh
wsl --install
wsl --list --online
wsl --install -d <Distribution Name>
```

After rebooting the machine, run the distro you installed from the Terminal application.
Set your user credentials, and configure git with the following commands:

```sh
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
ssh-keygen -t rsa -b 4096 -C “tu_email@gmail.com”
```

Remember to set up SSH in your GitHub account.

After that configure Terminal application with the following features:

* `Run as Administrator`
* `Nerd Font Mono`
* `Font Size 14`
* `Transparency 80%`
* `Color Background Black`

Now change the superuser password before you start modifying the terminal and other apps.

```sh
sudo su
passwd
exit
```

Now we will install zsh and create its configuration file using the file in this repo named zshrc:

```sh
sudo apt-get install zsh
sudo reboot now
vim ~/.zshrc
```

before sourcing the file for the system to read it and apply the changes, we will install the necessary dependencies:

```sh
sudo apt-get install lsd bat zsh-autosuggestions zsh-syntax-highlighting
source ~/.zshrc
```

Now we will create the space for the zsh-sudo plugin:

```sh
sudo su
cd /usr/share
mkdir zsh-sudo
chown user:group zsh-sudo
exit
cd /usr/share/zsh-sudo 
sudo apt-get install wget
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/plugins/sudo/sudo.plugin.zsh
```
Now we will install [powerlevel10k](https://github.com/romkatv/powerlevel10k):

```sh
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

Now we will install [NeoVim](https://github.com/neovim/neovim/blob/master/INSTALL.md):

```sh
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux64.tar.gz
sudo rm -rf /opt/nvim
sudo tar -C /opt -xzf nvim-linux64.tar.gz
```

Then we will add NeoVim to the Path in the .zshrc file:

```sh
/opt/nvim-linux64/bin
```

Now we will install [NvChad](https://nvchad.com/docs/quickstart/install/) as indicated in its official page in addition to installing C in the whole system:

```sh
sudo apt-get install build-essential
git config --global core.editor nvim
```

Now we will install MdCat using cargo:

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
cargo install mdcat
```
