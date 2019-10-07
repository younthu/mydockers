# mydockers
个人常用docker

## Samba

利用docker搭建samba服务器步骤:

1. 先运行docker 创建samba服务器容器
~~~
docker run -it --name samba -p 139:139 -p 445:445 -v $PWD/samba_shared:/shared -d dperson/samba -u 'dg;dg123' -u 'admin;admin_123' -s 'public;/shared/public' -s 'users;/shared/users;yes;no;yes;all;all;all'
~~~

或者用下面这种展开后的命令:
~~~
docker run -it --name samba -p 139:139 -p 445:445 -v $PWD/samba_shared:/shared -d dperson/samba \
-u 'dg; password’ \   #创建用户dg, 密码password
-u 'admin; password’ \  #创建用户admin, 密码password
-s 'public;/shared/public'   # 创建共享只读目录public,
-s 'users;/shared/users;yes;no;yes;all;all;all'   #创建共享可读可写目录
~~~

2. 给samba_share/users给与可写权限. host中运行`sudo chmod 777 samba_share/users`即可， 我们只需要users目录可写

上面这条命令会 把当前目录下的samba_shared加载到 容器/shared目录下面去，同时创建dg, 和admin两个用户, 然后创建public和users两个子共享目录, public目录是只读的, users目录是可写的.

注意: 
要在host下运行 `sudo chmod 777 samba_share/users` 命令，否则samba服务器会 认为users目录是不可写的，配置了samba权限也没有用, 这个问题坑了我几个小时时间。
