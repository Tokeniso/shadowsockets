# shadowsockets
基于官方提供的仓库v3.3.2，只调整了目录结构和相关docker配置。
```https://github.com/shadowsocks/shadowsocks-libev/tree/v3.3.2```
alpine目录对应官方位置
```/shadowsocks-libev/docker/alpine/```

# 安装
需要在宿主机安装docker与docker-compose。

进入alpine目录，运行```docker-compose up```

出现：
```
Creating alpine_shadowsocks_1...
Attaching to alpine_shadowsocks_1
shadowsocks_1 |  2019-10-14 03:25:25 INFO: UDP relay enabled
shadowsocks_1 |  2019-10-14 03:25:25 INFO: initializing ciphers... aes-256-cfb
shadowsocks_1 |  2019-10-14 03:25:25 INFO: using nameserver: 8.8.8.8,8.8.4.4
shadowsocks_1 |  2019-10-14 03:25:25 INFO: tcp server listening at 0.0.0.0:8388
shadowsocks_1 |  2019-10-14 03:25:25 INFO: udp server listening at 0.0.0.0:8388
```
代表安装成功，开放宿主机的8388端口，使用shadowsocket客户端就能连接了。
安装成功后会停留在进程启动介面，```CTRL + C ``` 然后查看docker容器的ID，运行```docker start ID``` 就行了。也可以直接```docker-compose up -d```后台运行。

# 注
docker-composer.yml
```
shadowsocks:
  image: shadowsocks/shadowsocks-libev
  ports:
    - "8388:8388/tcp" // 根据自己的想法自由调整端口
    - "8388:8388/udp" // 记得宿主机开放对应端口就行
  environment:
    - METHOD=aes-256-cfb        // 加密方式
    - PASSWORD=Any_YouWantPwd.  // 密码
  restart: always
```
