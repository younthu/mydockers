# 关于本docker
本docker是一个rails集成环境, 集成rails + puma + postgres + nginx. 

默认是ruby 2.5.5


# 使用

1. 把docker-compose.yml和docker/目录拷贝到rails跟目录下面去
1. docker-compose up -d app # 网站会在3000端口起来，环境为production
1. docker-compose down 可以销毁已经起来的容器
1. docker-compose build 会重新编译镜像文件.


# todo
1. 用thor自动拷贝生成本docker环境

# 
# 文件结构

<pre>
-app_name
  -app
  -db
  -config
    -database.yml
  ...
  -docker
    -app  # docker for rails app
      -DockerFile
    -web  # docker for nginx
      -DockerFile
      -nginx.conf
  -docker-compose.yml
 </pre>


1. [参考](https://itnext.io/docker-rails-puma-nginx-postgres-999cd8866b18)
