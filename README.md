# 说明文档

## coffeshop 微服务应用 启动流程

### Postgres 数据库启动流程

1. 由于该微服务应用将数据库整合进集群内部，故需提前设置挂载点

``` $ mkdir -p /var/k8s/postgres/data```

2. 使用该路径下的 postgres-volume.yaml 启动 postgres 数据库服务

``` $ kubectl apply -f ./postgres-volume.yaml ```

3. 稍等片刻，待微服务的 pod 和 svc 准备就绪后，
即可通过数据库客户端或可视化软件访问 IP:31432 端口访问数据库。

    数据库信息如下
    
    DB_NAME = coffeeshop
    DB_USERNAME = dbuser
    PASSWORD = love_coffee


### user-opers 数据资源层及 api 资源应用

1. 使用该路径下的 userops.yaml 启动该应用服务

``` $ kubectl apply -f userops.yaml```

2. 待相应的 pods 和 svc 准备就绪后，进入相应的 pod

``` $ kubectl exec -it <coffeeshop-useropers-hash-code> /bin/bash```

3. 在进入后的 pod 中，输入 flask-sqlalchemy 自动将数据库升级

``` docker-inside$ flask db upgrade```

