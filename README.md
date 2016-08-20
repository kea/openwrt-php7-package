PHP7 Package for OpenWrt


Compile PHP7 modules
====================

Follow the cross compile tutorial on the Omega site
https://wiki.onion.io/Tutorials/Cross-Compile

In the step 3, add the PHP7 repo

```
echo "src-git onion https://github.com/kea/openwrt-php7-package.git" >> feeds.conf.default
scripts/feeds update -a
scripts/feeds install php7
```

Install from ipk package for ar7xx
==================================

Note: I've tested this package only on Onion Omega.
If you don't want to cross complile yourself the package, you can skip the previous step and install the already compiled and packed files:

```
wget http://repo.k3a.it/omega/packages/key.pub && opkg-key add key.pub && rm key.pub
echo "src/gz chaos_calmer_php7 http://repo.k3a.it/omega/packages" >> /etc/opkg/distfeeds.conf
opkg update
opkg install php7-cli

php-cli -v
PHP 7.1.0 (cli) (built: Aug 18 2016 19:23:40) ( NTS )
Copyright (c) 1997-2016 The PHP Group
Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
```