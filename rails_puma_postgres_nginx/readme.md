# 关于本docker
本docker是一个rails集成环境, 集成rails + puma + postgres + nginx. 

默认是ruby 2.5.5, nodejs 6.16


# 使用

1. 把docker-compose.yml和docker/目录拷贝到rails跟目录下面去
1. docker-compose up -d app # 网站会在3000端口起来，环境为production
1. docker-compose down 可以销毁已经起来的容器
1. docker-compose build 会重新编译镜像文件.
1. 如果遇到js找不到的问题，请尝试运行 `RAILS_ENV=production bundle exec rake assets:precompile`

如果不需要起postgresq, 请把docker-compose.yml里面的以下内容删除:

~~~
depends_on:
      - db
~~~

# todo
1. 用thor自动拷贝生成本docker环境
1. 更新node的版本, 当前安装的是nodejs 6, 最新的nodejs已经到10了

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

# 问题解决

## 容器退出的问题
生产环境下可能会遇到`docker-compose up -d app`命令跑了以后容器马上退出了，这个时候可以通过`docker logs xxxxxxx`来查看容器日志，判断问题所在.

1. ! Unable to load application: ArgumentError: Missing `secret_key_base` for 'production' environment, set this string with `rails credentials:edit`
   解决方法: 
   1. rake secret 生成密码
   1. 把上面生成的内容放到config/secrets.yml里面去
      ~~~
      # config/secrets.yml
      production:
         secret_key_base: <上面生成的key>
      ~~~

    或者在Application.rb里面写死secret: `config.secret_key = 'f8fd45107e3f1cff9225a9250ebad5c63110f9888dc77bd5186f0870c003aff3b7aee4695387191cbc8da55d71b4f47c1f99b4d52cb2eb92c4f6a3523bd42812'
`
      
   或者有个更复杂先进的key管理方法: https://waiyanyoon.com/deploying-rails-5-2-applications-with-encrypted-credentials-using-capistrano/
1. ActionView::Template::Error (The asset "application.css" is not present in the asset pipeline.):
    1. 运行命令: `RAILS_ENV=production bundle exec rails assets:precompile`
    1. 重启docker, docker restart <container id>
      
# 参考
1. [参考](https://itnext.io/docker-rails-puma-nginx-postgres-999cd8866b18)

