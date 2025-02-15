![GitHub last commit](https://img.shields.io/github/last-commit/mrstandu33/ProcessusWebServ/master)
![GitHub repo size](https://img.shields.io/github/repo-size/mrstandu33/ProcessusWebServ)
[![GitHub license](https://img.shields.io/github/license/mrstandu33/ProcessusWebServ.svg)](https://github.com/mrstandu33/ProcessusWebServ/blob/master/LICENSE)

[![time tracker](https://wakatime.com/badge/github/mrstandu33/ProcessusWebServ.svg)](https://wakatime.com/badge/github/mrstandu33/ProcessusWebServ)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/3411c636196449839ed2f0fc94a52e9b)](https://www.codacy.com/manual/mrstandu33/ProcessusWebServ?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=mrstandu33/ProcessusWebServ&amp;utm_campaign=Badge_Grade)
![HitCount](http://hits.dwyl.io/mrstandu33/ProcessusWebServ.svg)

[![Twitch Status](https://img.shields.io/twitch/status/mrstandu33)](https://twitch.tv/mrstandu33)

# Table of content
<details>
  <ul>
    <li><a href="#table-of-content">Table of content</a></li>
    <li>
      <a href="#setup-instructions">Setup instructions</a>
      <ul>
        <li><a href="#install-web-server">Install Web Server</a></li>
        <li><a href="#setup-windows-terminal">Setup Windows Terminal</a></li>
        <li>
          <a href="#setup-wsl2">Setup WSL2</a>
          <ul>
            <li>
              <a href="#basics">Basics</a>
              <ul>
                <li><a href="#setup-wsl-behavior">Setup WSL behavior</a></li>
                <li><a href="#setup-zsh">Setup ZSH</a></li>
                <li><a href="#setup-github-ssh-key">Setup GitHub SSH Key</a></li>
                <li><a href="#setup-github-gpg-key">Setup GitHub GPG Key</a></li>
                <li><a href="#setup-pinentry-for-wsl">Setup Pinentry for WSL</a></li>
              </ul>
            </li>
            <li>
              <a href="#ease-of-use">Ease of use</a>
              <ul>
                <li><a href="#fix-apache24-apr_tcp_defer_accept-bug-in-wsl2">Fix Apache2.4 'APR_TCP_DEFER_ACCEPT' bug in WSL2</a></li>
                <li><a href="#setup-bash-aliases">Setup bash aliases</a></li>
                <li><a href="#setup-terminal-colors">Setup terminal colors</a></li>
                <li><a href="#setup-autoload-for-apache2">Setup autoload for Apache2</a></li>
                <li><a href="#setup-autoload-for-mysql">Setup autoload for MySQL</a></li>
                <li><a href="#setup-wakatime-api">Setup Wakatime API</a></li>
                <li><a href="#setup-powerline-go">Setup Powerline Go</a></li>
                <li><a href="#setup-archey4">Setup Archey4</a></li>
              </ul>
            </li>
          </ul>
        </li>
        <li><a href="#create-apache2-virtualhost">Create Apache2 VirtualHost</a></li>
        <li>
          <a href="#create-user">Create user</a>
          <ul>
            <li><a href="#mysql-user">MySQL user</a></li>
            <li><a href="#unix-user">Unix user</a></li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</details>

# Setup instructions

## Install Web Server

```bash
  $ apt-get update -y && \
  apt-get upgrade -y && \
  apt-get dist-upgrade -y && \
  apt-get install -y wget lsb-release apt-transport-https ca-certificates && \
  wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
  echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php7.4.list && \
  apt-get update -y && \
  apt-get install -y apache2 apache2-doc apache2-utils curl mariadb-server sendmail python3-pip git unzip emacs php7.4 php7.4-cli php7.4-fpm php7.4-json php7.4-pdo php7.4-mysql php7.4-zip php7.4-gd  php7.4-mbstring php7.4-curl php7.4-xml php7.4-bcmath php7.4-json libapache2-mod-php7.4 php-cli php-mbstring nodejs npm && \
  curl -sS https://getcomposer.org/installer -o composer-setup.php && \
  php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
  a2enmod rewrite && \
  sendmailconfig && \
  service apache2 restart
```

## Setup Windows Terminal
> https://www.microsoft.com/fr-fr/p/windows-terminal-preview/9n0dx20hk701
* Here is some basic configurations :
  ```json
  {
    "$schema": "https://aka.ms/terminal-profiles-schema",

    "alwaysShowTabs" : true,
    "defaultProfile" : "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
    "initialCols" : 120,
    "initialRows" : 30,
    "requestedTheme" : "system",
    "showTabsInTitlebar" : true,
    "showTerminalTitleInTitlebar" : true,
    "wordDelimiters" : " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502",
    "profiles" :
    [
      {
        "acrylicOpacity" : 0.60,
        "background" : "#111111",
        "backgroundImageOpacity" : 0.60,
        "backgroundImageStretchMode" : "uniformToFill",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "wsl.exe ~",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Cascadia Code PL",
        "fontSize" : 11,
        "guid" : "{58ad8b0c-3ef8-5f4d-bc6f-13e4c00f2530}",
        "historySize" : 9001,
        "name" : "Debian",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "tabTitle" : "Debian",
        "useAcrylic" : true
      },
      {
        "acrylicOpacity" : 0.60,
        "background" : "#111111",
        "backgroundImageOpacity" : 0.60,
        "backgroundImageStretchMode" : "uniformToFill",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "cmd.exe",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Cascadia Code PL",
        "fontSize" : 11,
        "guid" : "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}",
        "historySize" : 9001,
        "name" : "Command Prompt",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "startingDirectory" : "%USERPROFILE%",
        "tabTitle" : "Command Prompt",
        "useAcrylic" : true
      },
      {
        "acrylicOpacity" : 0.75,
        "background" : "#012456",
        "closeOnExit" : true,
        "colorScheme" : "Campbell",
        "commandline" : "powershell.exe",
        "cursorColor" : "#FFFFFF",
        "cursorShape" : "bar",
        "fontFace" : "Cascadia Code PL",
        "fontSize" : 11,
        "guid" : "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
        "historySize" : 9001,
        "name" : "Windows PowerShell",
        "padding" : "0, 0, 0, 0",
        "snapOnInput" : true,
        "startingDirectory" : "%USERPROFILE%",
        "tabTitle" : "Powershell",
        "useAcrylic" : true
      },
      {
          "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}",
          "hidden": true,
          "name": "Azure Cloud Shell",
          "source": "Windows.Terminal.Azure"
      }
    ],
    "schemes" :
    [
      {
        "background" : "#0C0C0C",
        "black" : "#0C0C0C",
        "blue" : "#0037DA",
        "brightBlack" : "#767676",
        "brightBlue" : "#3B78FF",
        "brightCyan" : "#61D6D6",
        "brightGreen" : "#16C60C",
        "brightPurple" : "#B4009E",
        "brightRed" : "#E74856",
        "brightWhite" : "#F2F2F2",
        "brightYellow" : "#F9F1A5",
        "cyan" : "#3A96DD",
        "foreground" : "#CCCCCC",
        "green" : "#13A10E",
        "name" : "Campbell",
        "purple" : "#881798",
        "red" : "#C50F1F",
        "white" : "#CCCCCC",
        "yellow" : "#C19C00"
      },
      {
        "background" : "#282C34",
        "black" : "#282C34",
        "blue" : "#61AFEF",
        "brightBlack" : "#5A6374",
        "brightBlue" : "#61AFEF",
        "brightCyan" : "#56B6C2",
        "brightGreen" : "#98C379",
        "brightPurple" : "#C678DD",
        "brightRed" : "#E06C75",
        "brightWhite" : "#DCDFE4",
        "brightYellow" : "#E5C07B",
        "cyan" : "#56B6C2",
        "foreground" : "#DCDFE4",
        "green" : "#98C379",
        "name" : "One Half Dark",
        "purple" : "#C678DD",
        "red" : "#E06C75",
        "white" : "#DCDFE4",
        "yellow" : "#E5C07B"
      },
      {
        "background" : "#FAFAFA",
        "black" : "#383A42",
        "blue" : "#0184BC",
        "brightBlack" : "#4F525D",
        "brightBlue" : "#61AFEF",
        "brightCyan" : "#56B5C1",
        "brightGreen" : "#98C379",
        "brightPurple" : "#C577DD",
        "brightRed" : "#DF6C75",
        "brightWhite" : "#FFFFFF",
        "brightYellow" : "#E4C07A",
        "cyan" : "#0997B3",
        "foreground" : "#383A42",
        "green" : "#50A14F",
        "name" : "One Half Light",
        "purple" : "#A626A4",
        "red" : "#E45649",
        "white" : "#FAFAFA",
        "yellow" : "#C18301"
      },
      {
        "background" : "#002B36",
        "black" : "#073642",
        "blue" : "#268BD2",
        "brightBlack" : "#002B36",
        "brightBlue" : "#839496",
        "brightCyan" : "#93A1A1",
        "brightGreen" : "#586E75",
        "brightPurple" : "#6C71C4",
        "brightRed" : "#CB4B16",
        "brightWhite" : "#FDF6E3",
        "brightYellow" : "#657B83",
        "cyan" : "#2AA198",
        "foreground" : "#839496",
        "green" : "#859900",
        "name" : "Solarized Dark",
        "purple" : "#D33682",
        "red" : "#DC322F",
        "white" : "#EEE8D5",
        "yellow" : "#B58900"
      },
      {
        "background" : "#FDF6E3",
        "black" : "#073642",
        "blue" : "#268BD2",
        "brightBlack" : "#002B36",
        "brightBlue" : "#839496",
        "brightCyan" : "#93A1A1",
        "brightGreen" : "#586E75",
        "brightPurple" : "#6C71C4",
        "brightRed" : "#CB4B16",
        "brightWhite" : "#FDF6E3",
        "brightYellow" : "#657B83",
        "cyan" : "#2AA198",
        "foreground" : "#657B83",
        "green" : "#859900",
        "name" : "Solarized Light",
        "purple" : "#D33682",
        "red" : "#DC322F",
        "white" : "#EEE8D5",
        "yellow" : "#B58900"
      }
    ]
  }
  ```


## Setup WSL2

### Basics

#### Setup WSL behavior
1. Type in Bash :
  ```bash
  $ emacs /etc/wsl.conf
  ```
2. Write inside the file :
  ```conf
  [automount]
  enabled = true
  options = "metadata,umask=22,fmask=11"
  [Interop]
  appendWindowsPath = True
  ```
3. Type in Command Prompt :
  ```bash
  > wsl -l
  # get wsl name
  > wsl -t $NANE
  > $NAME config --default-user root
  ```
---

#### Setup ZSH
1. Type in Bash :
  ```bash
  $ apt-get install -y zsh
  $ chsh
  $ /bin/zsh
  $ cd ~
  $ curl -L git.io/antigen > antigen.zsh
  $ emacs ~/.zshrc
  ```
2. Write inside the file :
  ```conf
  source ~/antigen.zsh

  antigen use oh-my-zsh

  antigen bundle git
  antigen bundle pip
  antigen bundle github
  antigen bundle npm
  antigen bundle command-not-found
  antigen bundle common-aliases
  antigen bundle compleat
  antigen bundle git-extras

  antigen bundle zsh-users/zsh-syntax-highlighting
  antigen bundle zsh-users/zsh-completions
  antigen bundle zsh-users/zsh-autosuggestions

  antigen apply
  ```
---
#### Setup GitHub SSH Key
> https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh
1. Type in Bash :
  ```bash
  $ ssh-keygen -t rsa -b 4096 -C "email@example.com"
  $ eval $(ssh-agent -s)
  $ ssh-add ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub
  # print on GitHub
  $ emacs ~/.bashrc
  ```
2. Write inside the file :
  ```bash
  ##### Start Auto start ssh-agent #####
  eval $(ssh-agent) > /dev/null 2>&1
  ##### End Auto start ssh-agent #####
  ```
---
#### Setup GitHub GPG Key
> https://help.github.com/en/github/authenticating-to-github/managing-commit-signature-verification
1. Type in Bash :
  ```bash
  $ gpg --full-generate-key
  $ gpg --list-secret-keys --keyid-format LONG
  $ gpg --armor --export $KEY # print on GitHub
  $ git config --global user.signingkey $KEY
  $ git config --global user.name "John Doe"
  $ git config --global user.email "email@example.com"
  # Set in VSCode settings.json -> "git.enableCommitSigning": true,
  ```
---
#### Setup Pinentry for WSL
> https://github.com/diablodale/pinentry-wsl-ps1
1. Type in Bash :
  ```bash
  $ cd ~
  $ git clone https://github.com/diablodale/pinentry-wsl-ps1
  $ cd pinentry-wsl-ps1/
  $ chmod ug=rx pinentry-wsl-ps1.sh
  $ emacs ~/.gnupg/gpg-agent.conf
  ```
2. Write inside the file :
  ```conf
  enable-ssh-support
  disable-scdaemon
  pinentry-program /root/pinentry-wsl-ps1/pinentry-wsl-ps1.sh
  debug 1024
  debug-pinentry
  log-file ~/agent.log
  ```
3. Type in Bash :
  ```bash
  $ gpg-connect-agent killagent /bye
  $ gpg-connect-agent /bye
  $ emacs ~/.bashrc
  ```
4. Write inside the file :
  ```bash
  ##### Start Pinentry-WSL-PS1 enabling #####
  export GPGKEY=3922899C9BCA4AE4 # set prefered gpg signing key
  PIDFOUND=$(pgrep gpg-agent)
  if [ -n "$PIDFOUND" ]; then
    export GPG_AGENT_INFO="~/.gnupg/S.gpg-agent:$PIDFOUND:1"
    export GPG_TTY=$(tty)
    export SSH_AUTH_SOCK="~/.gnupg/S.gpg-agent.ssh"
    unset SSH_AGENT_PID
  fi
  PIDFOUND=$(pgrep dirmngr)
  if [ -n "$PIDFOUND" ]; then
    export DIRMNGR_INFO="~/.gnupg/S.dirmngr:$PIDFOUND:1"
  fi
  unset PIDFOUND
  ##### End Pinentry-WSL-PS1 enabling #####
  ```
<br/>

### Ease of use
> https://github.com/microsoft/WSL/issues/1953
#### Fix Apache2.4 'APR_TCP_DEFER_ACCEPT' bug in WSL2
>
1. Type in Bash :
  ```bash
  $ emacs /etc/apache2/apache2.conf
  ```
2. Write inside the file :
  ```conf
  AcceptFilter https none
  AcceptFilter http none
  ```
3. Type in Bash :
  ```bash
  service apache2 restart
  ```

#### Setup bash aliases
1. Type in Bash :
  ```bash
  $ emacs ~/.bashrc
  ```
2. Write inside the file :
  ```bash
  ##### Start Aliases setup #####
  alias ssh="ssh -A"
  alias emacs="emacs -nw"
  ##### End Aliases setup #####
  ```
---
#### Setup terminal colors
1. Type in Bash :
  ```bash
  $ emacs ~/.bashrc
  ```
2. Write inside the file :
  ```bash
  ##### Start Terminal Color enabling #####
  eval "`dircolors`"
  force_color_prompt=yes
  alias ls='ls --color=auto'
  ##### End Terminal Color enabling #####
  ```
---
#### Setup autoload for Apache2
1. Type in Bash :
  ```bash
  $ emacs ~/.bashrc
  ```
2. Write inside the file :
  ```bash
  ##### Start Auto load Apache2 #####
  if [ $(service apache2 status | grep -v grep | grep 'apache2 is not running ... failed!' | wc -l) != 0 ]
  then
    su -c "printf '\n%s\n' 'Starting Apache2.4 service...' && service apache2 start && printf '%s\n' 'Started Apache2.4 service.'" root
  else
    su -c "printf '\n%s\n' 'Apache2.4 service already started.'" root
  fi
  ##### End Auto load Apache2 #####
  ```
---
#### Setup autoload for MySQL
1. Type in Bash :
  ```bash
  $ emacs ~/.bashrc
  ```
2. Write inside the file :
  ```bash
  ##### Start Auto load MySQL #####
  if [ $(service mysql status | grep -v grep | grep 'MariaDB is stopped..' | wc -l) != 0 ]
  then
    su -c "printf '\n%s\n' 'Starting mysql9.1 service...' && service mysql start && printf '%s\n' 'Started mysql9.1 service.'" root
  else
    su -c "printf '\n%s\n' 'Mysql9.1 service already started.'" root
  fi
  ##### End Auto load MySQL #####
  ```
---
#### Setup Wakatime API
> https://wakatime.com/terminal#install-bash
1. First :
    * If you uses zsh :
      1. Type in Bash :
        ```bash
        $ emacs ~/.zshrc
        ```
      2. Write inside the file :
        ```bash
        antigen bundle sobolevn/wakatime-zsh-plugin
        ```
    * If you uses bash :
      1. Type in Bash :
        ```bash
        $ cd ~
        $ git clone https://github.com/gjsheep/bash-wakatime.git
        $ emacs ~/.bashrc
        ```
      2. Write inside the file :
        ```bash
        ##### Start Wakatime enabling #####
        source ~/bash-wakatime/bash-wakatime.sh
        ##### End Wakatime enabling #####
        ```
2. Visit https://wakatime.com/settings/account and copy your API KEY
3. Type in Bash :
  ```bash
  $ pip3 install wakatime
  $ emacs ~/.wakatime.cfg
  ```
4. Write inside the file :
  ```conf
  [settings]
  api_key = $API_KEY
  ```
---
#### Setup Powerline Go
> https://github.com/justjanne/powerline-go
1. First :
    * If you uses zsh :
      1. Type in Bash :
        ```bash
        $ emacs ~/.zshrc
        ```
      2. Write inside the file :
        ```bash
        antigen bundle Lokaltog/powerline powerline/bindings/zsh
        ```
      3. Type in Bash :
        ```bash
        $ pip3 install powerline-status
        ```
    * If you uses bash :
      1. Type in Bash :
        ```bash
        $ apt-get install golang -y
        $ go get -u github.com/justjanne/powerline-go
        $ emacs ~/.bashrc
        ```
      2. Write inside the file :
        ```bash
        ##### Start Powerline Go enabling #####
        GOPATH=~/go
        function _update_ps1() {
          PS1="$($GOPATH/bin/powerline-go -error $?)"
        }
        if [ "$TERM" != "linux" ] && [ -f "$GOPATH/bin/powerline-go" ]; then
          PROMPT_COMMAND="_update_ps1; $PROMPT_COMMAND"
        fi
        ##### End Powerline Go enabling #####
        ```
2. Visit https://github.com/microsoft/cascadia-code/releases, download `CascadiaPL.ttf` and install it on Windows
---
#### Setup Archey4
> https://github.com/HorlogeSkynet/archey4
1. Type in Bash :
  ```bash
  $ pip3 install archey4
  $ emacs /etc/archey4/config.json
  ```
2. Write inside the file :
  ```json
  {
    "allow_overriding": true,
    "suppress_warnings": true,
    "entries": {
      "User": true,
      "Hostname": true,
      "Model": false,
      "Distro": true,
      "Kernel": true,
      "Uptime": true,
      "WindowManager": false,
      "DesktopEnvironment": false,
      "Shell": true,
      "Terminal": true,
      "Packages": true,
      "Temperature": false,
      "CPU": true,
      "GPU": false,
      "RAM": true,
      "Disk": true,
      "LAN_IP": true,
      "WAN_IP": true
    },
    "colors_palette": {
      "use_unicode": true
    },
    "default_strings": {
      "no_address": "No Address",
      "not_detected": "Not detected",
      "virtual_environment": "Virtual Environment",
      "bare_metal_environment": "Bare-metal Environment"
    },
    "ip_settings": {
      "lan_ip_max_count": 2,
      "wan_ip_v6_support": false
    },
    "limits": {
      "ram": {
        "warning": 33.3,
        "danger": 66.7
      },
      "disk": {
        "warning": 50,
        "danger": 75
      }
    },
    "temperature": {
      "char_before_unit": "°",
      "use_fahrenheit": false
    },
    "timeout": {
      "ipv4_detection": 1,
      "ipv6_detection": 1
    }
  }
  ```
3. Type in Bash :
  ```bash
  $ emacs ~/.bashrc
  ```
4. Write inside the file :
  ```bash
  ##### Start Archey enabling #####
  archey
  ##### End Archey enabling #####
  ```
<br/>

## Create Apache2 VirtualHost
1. Type in Bash :
  ```bash
  $ emacs /etc/apache2/sites-available/sub.domain.ext.conf
  ```
2. Write inside the file :
  ```conf
  <VirtualHost *:80>
    ServerName sub.domain.ext
    #ServerAlias sub2.domain.ext only if necessary
    DocumentRoot /var/www/sub.domain.ext/

    ErrorLog /var/log/apache2/sub.domain.ext.error.log
    CustomLog /var/log/apache2/sub.domain.ext.access.log combined
  </VirtualHost>
  ```
3. Type in Bash :
  ```bash
  $ a2ensite sub.domain.ext
  $ service apache2 restart
  ```
<br/>

## Create user

### MySQL user
1. Type in Bash :
  ```bash
  $ mysql -u root -p
  ```
2. Type in SQL prompt :
  ```SQL
  > CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
  > CREATE DATABASE database;
  > GRANT ALL PRIVILEGES ON database.* TO 'user'@'localhost';
  > FLUSH PRIVILEGES;
  > exit;
  ```

### Unix user
1. Type in Bash :
  ```bash
  $ NEWUSER=nomprenom
  $ useradd -m -s /bin/bash $NEWUSER
  $ chmod 755 /home/$NEWUSER
  $ rm /home/$NEWUSER/.bashrc
  $ usermod -g www-data $NEWUSER
  $ emacs /home/$NEWUSER/.bash_profile
  ```
2. Write inside the file :
  ```bash
  alias ls='ls --color=auto'
  ##### Start Alias access blocking #####
  alias su="printf ''"
  alias sudo="printf ''"
  alias apt-get="printf ''"
  alias aptitude="printf ''"
  alias exit="printf ''"
  alias logout="printf ''"
  alias passwd="printf ''"
  alias rlogin="printf ''"
  alias ssh="printf ''"
  alias slogin="printf ''"
  alias yppasswd="printf ''"
  alias mail="printf ''"
  alias mesg="printf ''"
  alias pine="printf ''"
  alias talk="printf ''"
  alias write="printf ''"
  alias as="printf ''"
  alias awk="printf ''"
  alias bc="printf ''"
  alias cc="printf ''"
  alias csh="printf ''"
  alias dbx="printf ''"
  alias f77="printf ''"
  alias gdb="printf ''"
  alias gprof="printf ''"
  alias kill="printf ''"
  alias ld="printf ''"
  alias lex="printf ''"
  alias lint="printf ''"
  alias make="printf ''"
  alias maple="printf ''"
  alias math="printf ''"
  alias nice="printf ''"
  alias nohup="printf ''"
  alias pc="printf ''"
  alias perl="printf ''"
  alias prof="printf ''"
  alias python="printf ''"
  alias sh="printf ''"
  alias yacc="printf ''"
  alias xcalc="printf ''"
  alias apropos="printf ''"
  alias find="printf ''"
  alias info="printf ''"
  alias man="printf ''"
  alias whatis="printf ''"
  alias whereis="printf ''"
  alias chmod="printf ''"
  alias chown="printf ''"
  alias chgrp="printf ''"
  alias cmp="printf ''"
  alias comm="printf ''"
  alias cp="printf ''"
  alias crypt="printf ''"
  alias diff="printf ''"
  alias file="printf ''"
  alias grep="printf ''"
  alias gzip="printf ''"
  alias ln="printf ''"
  alias lsof="printf ''"
  alias mkdir="printf ''"
  alias mv="printf ''"
  alias pwd="printf ''"
  alias quota="printf ''"
  alias rm="printf ''"
  alias rmdir="printf ''"
  alias stat="printf ''"
  alias sync="printf ''"
  alias sort="printf ''"
  alias tar="printf ''"
  alias tee="printf ''"
  alias tr="printf ''"
  alias umask="printf ''"
  alias uncompress="printf ''"
  alias uniq="printf ''"
  alias cat="printf ''"
  alias fold="printf ''"
  alias head="printf ''"
  alias lpq="printf ''"
  alias lpr="printf ''"
  alias lprm="printf ''"
  alias more="printf ''"
  alias less="printf ''"
  alias page="printf ''"
  alias pr="printf ''"
  alias tail="printf ''"
  alias zcat="printf ''"
  alias xv="printf ''"
  alias gv="printf ''"
  alias xpdf="printf ''"
  alias ftp="printf ''"
  alias rsync="printf ''"
  alias scp="printf ''"
  alias alias="printf ''"
  alias chquota="printf ''"
  alias chsh="printf ''"
  alias clear="printf ''"
  alias echo="printf ''"
  alias pbm="printf ''"
  alias popd="printf ''"
  alias pushd="printf ''"
  alias script="printf ''"
  alias setenv="printf ''"
  alias stty="printf ''"
  alias netstat="printf ''"
  alias rsh="printf ''"
  alias ssh="printf ''"
  alias bg="printf ''"
  alias fg="printf ''"
  alias jobs="printf ''"
  alias ^y="printf ''"
  alias ^z="printf ''"
  alias clock="printf ''"
  alias date="printf ''"
  alias df="printf ''"
  alias du="printf ''"
  alias env="printf ''"
  alias finger="printf ''"
  alias history="printf ''"
  alias last="printf ''"
  alias lpq="printf ''"
  alias manpath="printf ''"
  alias printenv="printf ''"
  alias ps="printf ''"
  alias pwd="printf ''"
  alias set="printf ''"
  alias spend="printf ''"
  alias stty="printf ''"
  alias time="printf ''"
  alias top="printf ''"
  alias uptime="printf ''"
  alias w="printf ''"
  alias who="printf ''"
  alias whois="printf ''"
  alias whoami="printf ''"
  alias gimp="printf ''"
  alias xfig="printf ''"
  alias xv="printf ''"
  alias xvscan="printf ''"
  alias xpaint="printf ''"
  alias kpaint="printf ''"
  alias mplayer="printf ''"
  alias realplay="printf ''"
  alias timidity="printf ''"
  alias xmms="printf ''"
  alias abiword="printf ''"
  alias addbib="printf ''"
  alias col="printf ''"
  alias diction="printf ''"
  alias diffmk="printf ''"
  alias dvips="printf ''"
  alias explain="printf ''"
  alias grap="printf ''"
  alias hyphen="printf ''"
  alias ispell="printf ''"
  alias latex="printf ''"
  alias pdfelatex="printf ''"
  alias latex2html="printf ''"
  alias lookbib="printf ''"
  alias macref="printf ''"
  alias ndx="printf ''"
  alias neqn="printf ''"
  alias nroff="printf ''"
  alias pic="printf ''"
  alias psdit="printf ''"
  alias ptx="printf ''"
  alias refer="printf ''"
  alias roffbib="printf ''"
  alias sortbib="printf ''"
  alias spell="printf ''"
  alias ispell="printf ''"
  alias style="printf ''"
  alias tbl="printf ''"
  alias tex="printf ''"
  alias tpic="printf ''"
  alias wget="printf ''"
  alias grabmode="printf ''"
  alias import="printf ''"
  alias xdpyinfo="printf ''"
  alias xkill="printf ''"
  alias xlock="printf ''"
  alias xterm="printf ''"
  alias xwininfo="printf ''"
  alias html2ps="printf ''"
  alias latex2html="printf ''"
  alias lynx="printf ''"
  alias netscape="printf ''"
  alias sitecopy="printf ''"
  alias weblint="printf ''"
  alias vi="vi -Z" #this is vi's safe mode and shell commands won't be run from within vi
  alias alias="printf ''"
  ##### End Alias access blocking #####
  ```
3. Type in Bash :
  ```bash
  $ chown root:root /home/$NEWUSER/.bash_profile
  $ chmod 755 /home/$NEWUSER/.bash_profile
  $ ssh-keygen
  ```
  * If user uses Windows system, or will use FileZilla (or any program that use .ppk key files) :
    <ul>
      <li>Download /home/$NEWUSER/.ssh/id_rsa</li>
      <li>Download PuTTY</li>
      <li>Install PuTTYgen and open it</li>
      <li>Click on `Conversions` > `Import key`</li>
      <li>Type passphrase</li>
      <li>Export private key to .ppk format</li>
    </ul>
4. Type in Bash :
  ```bash
  $ cat /home/$NEWUSER/.ssh/id_rsa.pub >> /home/$NEWUSER/.ssh/authorized_keys
  $ chmod -R go= /home/$NEWUSER/.ssh/
  $ chown -R $NEWUSER:$NEWUSER /home/$NEWUSER/.ssh/
  ```
