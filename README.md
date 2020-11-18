# Run multiple versions of PHP simotaneously

> This repo is cloned forked from `https://github.com/chialab/docker-php`.
> I only keep the `fpm` ones.

把 docker-phpinfo.conf 软链到 nginx 站点配置里, 然后这样查看 phpinfo 试试

http://你的ip:8000/php54.php

`54` 为 php 版本.

比如 build 一个 5.4 版本的.

```sh
# build
docker build -t shrekuu/php-fpm:5.4 .

# 跑起来(注意顺序, container 容器名放最后)
docker run -d -v /var/www:/var/www -p 9054:9000 shrekuu/php-fpm:5.4
```
