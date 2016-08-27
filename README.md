PHP7 Package for OpenWrt

TL;DR: Install from ipk package (ar7xx)
=======================================

Note: I've tested this package only on Onion Omega.
If you want to cross compile yourself the package, go to "Compile PHP7 module" 

Install PHP CLI
---------------

```
root@Omega-xxxx:~# wget http://repo.k3a.it/omega/packages/key.pub && opkg-key add key.pub && rm key.pub
root@Omega-xxxx:~# echo "src/gz kea_php7 http://repo.k3a.it/omega/packages" >> /etc/opkg/distfeeds.conf
root@Omega-xxxx:~# opkg update
root@Omega-xxxx:~# opkg install php7-cli
root@Omega-xxxx:~# php-cli -v
PHP 7.0.10 (cli) (built: Aug 27 2016 23:40:50) ( NTS )
Copyright (c) 1997-2016 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
```

Install Omega PHP module
------------------------

```
root@Omega-xxxx:~# opkg install php7-mod-onion-omega
root@Omega-xxxx:~# php-cli -m | grep omega
omega
```

Compile PHP7 modules
====================

Follow the cross compile tutorial on the Omega site
https://wiki.onion.io/Tutorials/Cross-Compile

In the step 3, add the PHP7 repo

```
echo "src-git kea_php7 https://github.com/kea/openwrt-php7-package.git" >> feeds.conf.default
scripts/feeds update -a
scripts/feeds install php7
```
