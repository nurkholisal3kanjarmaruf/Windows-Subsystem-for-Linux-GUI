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
