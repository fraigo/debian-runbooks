
## Install PEAR

Download

```bash
curl -O http://pear.php.net/go-pear.phar
sudo php -d detect_unicode=0 go-pear.phar
```

* Use option [`1`] to change path to [`/usr/local/pear`]
* Use option [`4`] to change path to [`/usr/local/bin`]


Check installation using:

```
pear version
```


## Install XDebug

```
brew install autoconf
```


```
sudo pecl install xdebug
```

Take note of the location of xdebug.so during installation and add or modify the following line to the `php.ini` file
using your xdebug.so path from the previous installation.

```
zend_extension="/usr/local/php/extensions/no-debug-zts-20160303/xdebug.so"
```

Check installation using this command (a list of xdebug configurations will be shown)

```
php -i |  grep xdebug
```
