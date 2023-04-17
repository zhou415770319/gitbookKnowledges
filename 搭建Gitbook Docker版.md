# 搭建Gitbook Docker版

Docker搭建gitbook服务
GitBook
Gitbooks简介
GitBook 是一个基于 Node.js 的命令行工具，可使用 Github/Git 和 Markdown 来制作精美的电子书，GitBook 并非关于 Git 的教程。
GitBook支持输出多种文档格式
静态站点：GitBook默认输出该种格式，生成的静态站点可直接托管搭载Github Pages服务上；
PDF：需要安装gitbook-pdf依赖
eBook：需要安装ebook-convert；
单HTML网页：支持将内容输出为单页的HTML，不过一般用在将电子书格式转换为PDF或eBook的中间过程；
JSON：一般用于电子书的调试或元数据提取。
GitBook基础文件
使用GitBook制作电子书，必备两个文件：README.md&SUMMARY.md。
Docker安装Gitbook
查找gitbook镜像

```
docker@default:~$ docker search -s 3 gitbook
NAME                         DESCRIPTION                               STARS     OFFICIAL   AUTOMATED
fellah/gitbook               GitBook                                   9                    [OK]
tobegit3hub/gitbook-server                                             7                    [OK]
fellah/gitbook-ebook                                                   3                    [OK]
billryan/gitbook             Docker for GitBook with Unicode support   3                    [OK]

```

安装gitbook镜像,官方镜像下载太慢的话可以使用国内的daocloud

```
docker@default:~$ docker pull fellah/gitbook
```

获取gitbook静态html文件，/yourpath下需要有README.md和SUMMARY.md文件。

```
docker run -v /yourpath:/srv/gitbook -v /yourpath/html:/srv/html fellah/gitbook gitbook build . /srv/html
```

展示Gitbook文件
因为生成的是html静态页面所以需要一个web服务来显示，当前选择用nginx。搜索nginx镜像

```
docker@default:~$ docker search -s 3 nginx
NAME                                     DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
nginx                                    Official build of Nginx.                        3350      [OK]
jwilder/nginx-proxy                      Automated Nginx reverse proxy for docker c...   691                  [OK]
richarvey/nginx-php-fpm                  Container running Nginx + PHP-FPM capable ...   215                  [OK]
jrcs/letsencrypt-nginx-proxy-companion   LetsEncrypt container to use with nginx as...   71                   [OK]
million12/nginx-php                      Nginx + PHP-FPM 5.5, 5.6, 7.0 (NG), CentOS...   67                   [OK]
maxexcloo/nginx-php                      Docker framework container with Nginx and ...   57                   [OK]
webdevops/php-nginx                      Nginx with PHP-FPM                              42                   [OK]
h3nrik/nginx-ldap                        NGINX web server with LDAP/AD, SSL and pro...   27                   [OK]
bitnami/nginx                            Bitnami nginx Docker Image                      18                   [OK]
maxexcloo/nginx                          Docker framework container with Nginx inst...   7                    [OK]
webdevops/nginx                          Nginx container                                 5                    [OK]
million12/nginx                          Nginx: extensible, nicely tuned for better...   5                    [OK]
evild/alpine-nginx                       Minimalistic Docker image with Nginx            4                    [OK]
webdevops/hhvm-nginx                     Nginx with HHVM                                 3                    [OK]
ixbox/nginx                              Nginx on Alpine Linux.                          3                    [OK]

```

安装nginx

注意：系统是linux的话在这就已经完成了，Mac和windows还需要配置端口转发，配置本地和docker的虚拟机之间的端口映射。
gitbook镜像地址&
nginx镜像地址
————————————————
版权声明：本文为CSDN博主「唐伯虎电蚯蚓」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_37348649/article/details/109353435

```
docker pull nginx
docker run --name my-nginx -v /yourpath/html:/usr/share/nginx/html -d -p 8080:80 nginx

```

注意：系统是linux的话在这就已经完成了，Mac和windows还需要配置端口转发，配置本地和docker的虚拟机之间的端口映射。
gitbook镜像地址&
nginx镜像地址
————————————————
版权声明：本文为CSDN博主「唐伯虎电蚯蚓」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_37348649/article/details/109353435