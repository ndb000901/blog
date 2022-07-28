# Mysql 安装



```sh
docker pull mysql:8.0.30

docker run -d -p 3306:3306 --privileged=true -v /home/hello/local/docker/tmp/mysql/log:/var/log/mysql -v /home/hello/local/docker/tmp/mysql/data:/var/lib/mysql -v /home/hello/local/docker/tmp/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=root --name mysql mysql:8.0.30
```









# Redis安装



```sh
docker pull redis:6.2.7
docker run -p 6379:6379 --name redis --privileged=true -v /home/hello/local/docker/tmp/redis/data/:/data -d redis:6.2.7 redis-server /home/hello/local/docker/tmp/redis/redis.conf 
d8462145308af71aad04179cc1805e9507e6c25b86f894f8a6657ab902a19b19
```





