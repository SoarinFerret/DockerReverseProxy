# Docker Reverse Proxy
This builds off of the wonderful work of [JrCs's letsencrypt](https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion/tree/stable) and [jcase's nginx-proxy](https://github.com/jwilder/nginx-proxy). Essentially, this allows for easy proxying of external services.

## IPTablesProxy
IPTables is a quick invention using iptables allowing proxying of external services. While technically it can be used for things other than webservices, in this specific case it is primarily used for web services. To run it on its own:
```
$ cd ./iptabesproxy
$ docker build -t iptablesproxy .
$ docker run -it --rm -e SERVERIP='172.217.9.46' -e SERVERPORT='80' -e HOSTPORT='80' --cap-add=NET_ADMIN --cap-add=NET_RAW -p 8080:80 siteproxy
```
A sample docker-compose file is provided to show how to use it with Let'sEncrypt and Nginx-Proxy. The "Test" service uses Let'sEncrypt, while "Test2" only uses the reverse proxy portion. This is useful in scenarios where the host is already providing SSL and don't want it to use Let'sEncrypt.