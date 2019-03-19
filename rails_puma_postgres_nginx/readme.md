# 关于本docker
本docker是一个rails集成环境, 集成rails + puma + postgres + nginx


# todo
1. 用thor自动拷贝生成本docker环境

# 
# 文件结构
Create docker folder in app root 

-app_name
  -app
  -db
  -config
    -database.yml
  ...
  -docker
    -app
      -DockerFile
    -web
      -DockerFile
      -nginx.conf
  -docker-compose.yml


1. [参考](https://itnext.io/docker-rails-puma-nginx-postgres-999cd8866b18)
