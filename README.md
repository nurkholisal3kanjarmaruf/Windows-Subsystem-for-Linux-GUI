# Windows-Subsystem-for-Linux-GUI

![Alt text](https://learn.microsoft.com/id-id/windows/images/windows-linux-dev-env.png)

### Setup User

### What is WSL and Install
https://learn.microsoft.com/en-us/windows/wsl/install

### Distro Linux
https://www.niagahoster.co.id/blog/distro-linux-terbaik/

### Linux Grapick and CLI Desktop Environment
https://revou.co/kosakata/cli
https://www.gnome.org/
https://kde.org/id/
https://www.xfce.org/


### 1. Upgrade
sudo apt update 
sudo apt -y upgrade

### 2. Install essentials
sudo apt install build-essential
sudo apt install net-tools
sudo apt install xrdp -y && sudo systemctl enable xrdp # remote desktop utilities


### 3. Setup GUI
sudo apt install -y tasksel
sudo tasksel install xubuntu-desktop
sudo apt install gtk2-engines

## Or


### 3.1 Setup GUI
!WSL commands:
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
wsl --set-default-version 2

!Ubuntu GUI commands:
sudo apt update && sudo apt -y upgrade
sudo apt-get purge xrdp
sudo apt install -y xrdp
sudo apt install -y xfce4
sudo apt install -y xfce4-goodies

sudo cp /etc/xrdp/xrdp.ini /etc/xrdp/xrdp.ini.bak
sudo sed -i 's/3389/3390/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/max_bpp=32/#max_bpp=32\nmax_bpp=128/g' /etc/xrdp/xrdp.ini
sudo sed -i 's/xserverbpp=24/#xserverbpp=24\nxserverbpp=128/g' /etc/xrdp/xrdp.ini
echo xfce4-session > ~/.xsession

sudo nano /etc/xrdp/startwm.sh
!comment these lines to:
#test -x /etc/X11/Xsession && exec /etc/X11/Xsession
#exec /bin/sh /etc/X11/Xsession

!add these lines:
startxfce4

sudo /etc/init.d/xrdp start

!Now in Windows, use Remote Desktop Connection
localhost:3390

!Then login using your Ubuntu username and password

!Good links:
Microsoft GUI announcement: https://devblogs.microsoft.com/commandline/the-windows-subsystem-for-linux-build-2020-summary/
Ubuntu WSL2 GUI Install:
https://dev.to/darksmile92/linux-on-windows-wsl-with-desktop-environment-via-rdp-522g
WSL 2 install: https://docs.microsoft.com/en-us/windows/wsl/install-win10
Docker for WSL2: https://docs.docker.com/docker-for-windows/wsl/
What is WSL? https://docs.microsoft.com/en-us/windows/wsl/about
WSL documentation: https://docs.microsoft.com/en-us/windows/wsl/
WSL 2 Announcement: https://devblogs.microsoft.com/commandline/announcing-wsl-2/


### 4. Export GUI config (add this to .bashrc)
export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0
export LIBGL_ALWAYS_INDIRECT=1
sudo /etc/init.d/dbus start &> /dev/null


### 5. Optional: add user to sudoers
sudo nano /etc/sudoers.d/dbus
add the below line and uncomment
your_user_name ALL = (root) NOPASSWD: /etc/init.d/dbus
Go to no. 11 in `1.windows-steps.ps1`

### 6. Run firefox in the background
firefox &

### 7. Optional: run xfce4 desktop
Change VcXsrv (in Windows) display settings to "One large window" or "Full screen"
xfce4-session

### If Get Another Problem
https://github.com/microsoft/WSL/issues/5406
https://homanhuang.medium.com/install-ubuntu-on-windows-10-pro-f4bf7d6ebc99
https://askubuntu.com/questions/1380253/where-is-wsl-located-on-my-computer
https://learn.microsoft.com/id-id/windows/wsl/basic-commands
https://www.awonapa.com/2021/06/cara-copy-paste-di-virtualbox.html
