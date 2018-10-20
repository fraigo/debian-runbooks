
## Install PEAR

Download

```bash
curl -O http://pear.php.net/go-pear.phar
sudo php -d detect_unicode=0 go-pear.phar
```

Use option [`1`] to change path to [`/usr/local/pear`]
Use option [`4`] to change path to [`/usr/local/bin`]

Check installation using:

```
pear version
```


## Install XDebug

```
sudo pecl install xdebug
```

Add or modify the following line to the `php.ini` file

```
zend_extension="/usr/local/php/modules/xdebug.so"
```
