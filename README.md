# docker-nginx-google-proxy

Build a very tiny nginx image with google-proxy.

Demo site: [https://gg.bingozb.com](https://gg.bingozb.com/) (The service will be suspended at any time.)

## Build

You can pull the image from `hub.docker.com`.

```sh
$ docker pull bingozb/nginx-google-proxy
```

The image is only 7.72 MB. If you're in China, you can try to pull it from aliyuncs, which will be faster.

```sh
$ docker pull registry.cn-shenzhen.aliyuncs.com/bingozb/nginx-google-proxy
```

Or, you can build with source repository by yourself.

```sh
$ git clone https://github.com/bingozb/docker-nginx-google-proxy.git
$ cd docker-nginx-google-proxy
$ docker build -t bingozb/nginx-google-proxy .
```

## Usage

First, run a container with `bingozb/nginx-google-proxy` image.

```sh
$ sudo docker run --restart always -d --name nginx-google-proxy bingozb/nginx-google-proxy
```

Then, run your nginx container and link with `nginx-google-proxy`. eg. :

```sh
$ sudo docker run --restart always -d --name nginx \
-p 80:80 -p 443:443 \
--link nginx-google-proxy:google-proxy \
-v path/to/nginx.conf:/etc/nginx/conf.d/default.conf \
nginx
```

And your `path/to/nginx.conf` should be like this:

```sh
server {
    listen 80;
    server_name gg.bingozb.com;
    location ~ {
        proxy_pass http://google-proxy;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Ssl off;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Port 80;
    }
}
```

As you see, `google-proxy` is an alias for your nginx container and `nginx-google-proxy` link in the previous step.

## Correlation

- Dockerfile https://github.com/bingozb/docker-nginx-google-proxy/tree/master/Dockerfile
- Docker image https://hub.docker.com/r/bingozb/nginx-google-proxy/
- ngx_http_google_filter_module https://github.com/cuber/ngx_http_google_filter_module
- ngx_http_substitutions_filter_module https://github.com/yaoweibin/ngx_http_substitutions_filter_module



