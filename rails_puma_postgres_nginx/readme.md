# 关于本docker
本docker是一个rails集成环境, 集成rails + puma + postgres + nginx


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
