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





# ElasticSearch 安装



```
docker pull elasticsearch:7.17.6
docker network create es-net
docker run -d --name es --net es-net -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.17.6
```



# Kibana 安装



```
docker pull kibana:7.17.6
docker run -d --name kibana --net es-net -p 5601:5601 -e "ELASTICSEARCH_HOSTS=http://192.168.43.101:9200" kibana:7.17.6
```



# Portainer 安装



```
docker pull portainer/portainer-ce

docker run -p 9000:9000 -p 8000:8000 --name portainer \           20:39:09
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v /home/hello/local/docker/tmp/portainer:/data \
-d portainer/portainer-ce

```

