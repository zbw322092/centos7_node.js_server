# Build node.js server enviorment
Install a series of packages
``` bash
sudo yum install vim openssl build-essential libssl-dev wget curl git
```

`OpenSSL`
>OpenSSL is a cryptography toolkit implementing the Secure Sockets Layer ( SSL v2/v3) and Transport Layer Security ( TLS v1) network protocols and related cryptography standards required by them.
>The openssl program is a command line tool for using the various cryptography functions of OpenSSL's crypto library from the shell.

`wget`
> wget is a free utility for non-interactive download of files from the web. It supports HTTP, HTTPS, and FTP protocols, as well as retrieval through HTTP proxies.<br/>


And then, install `NVM`
https://github.com/creationix/nvm
> Node Version Manager - Simple bash script to manage multiple active node.js versions
``` bash
wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash
```

Then, using `NVM` to install `node.js`.
``` bash
nvm install v*.*.*
```

Now, we would like to increasing the amount of inotify watchers. Listen uses inotify by default on Linux to monitor directories for changes.
https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers
Execute:
``` bash
echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p
```

Get your current inotify file watch limit:
``` bash
$ cat /proc/sys/fs/inotify/max_user_watches
```

How, we can install some widely used npm packages. I just install `pm2`.
``` bash
npm install -g pm2
```





