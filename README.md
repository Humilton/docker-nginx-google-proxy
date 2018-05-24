# docker-nginx-google-proxy

Build a very tiny nginx image with google-proxy, proxy docs.google.com.

Demo site: [https://web.yaoping.win](https://web.yaoping.win) (The service will be suspended at any time.)

## Build

You can pull the image from `hub.docker.com`.

```sh
$ docker pull humilton/nginx-google-proxy
```

The image is only 7.75 MB. You can build with source repository by yourself.

```sh
$ git clone https://github.com/humilton/docker-nginx-google-proxy.git
$ cd docker-nginx-google-proxy
$ docker build -t humilton/nginx-google-proxy .
```

## Usage

First, use your own domain in nginx.conf
```
# vi nginx.conf
```
use command `:s/web.yaoping.win/<your domain replace google.com>/g`

use command `:s/w.yaoping.win/<your domain replace docs.google.com>/g`

use command `:s/api.yaoping.win/<your domain replace apis.google.com>/g`


Second, run a container with `humilton/nginx-google-proxy` image.

```sh
$ docker-compose up   # run `docker-compose up -d` for run as daemon
$ docker-compose down  # shutdown
```
Your server will start at port 8010
 
## Correlation

- Dockerfile https://github.com/bingozb/docker-nginx-google-proxy/tree/master/Dockerfile
- Docker image https://hub.docker.com/r/bingozb/nginx-google-proxy/
- ngx_http_google_filter_module https://github.com/cuber/ngx_http_google_filter_module
- ngx_http_substitutions_filter_module https://github.com/yaoweibin/ngx_http_substitutions_filter_module



