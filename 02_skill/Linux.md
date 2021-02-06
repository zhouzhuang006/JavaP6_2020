# Linux基础

















# 随学随用



## Ngnix 相关

vim /usr/local/nginx/conf/nginx.conf

/usr/local/nginx/sbin/nginx -t

/usr/local/nginx/sbin/nginx -s reload



## 定时重启执行gitbook服务

背景：由于采用github + Typara + gitbook 搭建的个人博客， 每次更新比较麻烦， 需要提交到github , 拉去最新的数据到服务器， 还需要重启gitbook , 打算做成每天晚上9点拉去最新的提交， 自动重启。

废话不多，上代码：

新建一个 start.sh 文件

vim start.sh

```shell
killall node
git pull
# gitbook build
gitbook serve --port 9188 > log.log 2>&1 &
```

设置linux 的 **crontab**

```
crontab [-u username]　　　　//省略用户表表示操作当前用户的crontab
    -e      (编辑工作表)
    -l      (列出工作表里的命令)
    -r      (删除工作作)
```

最后一行添加

```sh
0 */1 * * * sh /root/app/JavaP6_2020/start.sh
```

重启crontab：systemctl restart crond.service

> 如果没有按照 crontab 请仔细百度安装： **yum -y install cron**

