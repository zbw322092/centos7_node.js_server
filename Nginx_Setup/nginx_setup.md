# Nginx Setup
## Basic steps
First of all, install it.
``` bash
sudo yum install nginx
```

After installation, start `nginx` service.
``` bash
sudo systemctl start nginx
```

Now, we can get access server via 80 port. However, it is default nginx welcome page.


References:<br/>
[1] https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7


## Nginx Config
Create config file in `conf.d` folder.
``` bash
cd /etc/nginx/conf.d/
sudo vi ******-****.conf
```

The files in `conf.d` folder, which with `.conf` suffix will be loaded by `nginx`. 

Making sure this command is commentted out in file `/etc/nginx/nginx.conf`
``` bash
include /etc/nginx/default.d/*.conf;
```


Setup `upstream`:
The official [defination](http://nginx.org/en/docs/http/ngx_http_upstream_module.html) of `upstream` is:
> The ngx_http_upstream_module module is used to define groups of servers that can be referenced by the proxy_pass, fastcgi_pass, uwsgi_pass, scgi_pass, and memcached_pass directives.

I found a clearer [explanation](https://stackoverflow.com/questions/5877929/what-does-upstream-mean-in-nginx) about it. It is actually relate to load balance.
example config:
``` bash
http {
  upstream myproject {
    server 127.0.0.1:8000 weight=3;
    server 127.0.0.1:8001;
    server 127.0.0.1:8002;    
    server 127.0.0.1:8003;
  }

  server {
    listen 80;
    server_name www.domain.com;
    location / {
      proxy_pass http://myproject;
    }
  }
}
```

References:<br/>
[1] https://www.digitalocean.com/community/tutorials/understanding-nginx-server-and-location-block-selection-algorithms<br/>


Check `nginx` config syntax
``` bash
sudo nginx -t
```

Reload `nginx`
``` bash
sudo nginx -s reload
```

Check `nginx` status
``` bash
sudo systemctl status nginx
```

Hide `nginx` version info.
add following command in `nginx.conf` file.
``` bash
server_tokens off;
```
https://www.atulhost.com/hide-nginx-version


If you encounter problems about `nginx`(In my case, I got *502 Bad Gateway*), you can check `nginx` logs like this:
``` bash
sudo tail -30 /var/log/nginx/error.log
```
I solved my problem using [following](https://stackoverflow.com/questions/23948527/13-permission-denied-while-connecting-to-upstreamnginx) solution:
``` bash
sudo setsebool -P httpd_can_network_connect 1
```

*502 Bad Gateway* diagram demonstration:<br/>
https://www.datadoghq.com/blog/nginx-502-bad-gateway-errors-php-fpm/


Further reading:<br/>
[1] https://www.nginx.com/resources/admin-guide/reverse-proxy/<br/>
[2] http://nginx.org/en/docs/http/ngx_http_proxy_module.html?&_ga=2.138917499.977488074.1500038611-775240997.1500038611#proxy_set_header


##todo
[1]  How To Set Up a Node.js Application for Production on Ubuntu 16.04
https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04 <br>

[2] Virtual Hosts on nginx (CSC309)
https://gist.github.com/soheilhy/8b94347ff8336d971ad0 <br>