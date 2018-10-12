### 这是PHP+openresty版，如果需要PHP+Tenginx请转到https://github.com/w303972870/Nginx-PHP.git

```
docker pull w303972870/openresty-php
```

### PHP相关目录
#### 日志目录：/data/php/logs
#### 默认php-fpm.conf：/data/php/conf/php-fpm.conf
#### 默认www.conf：/data/php/conf/php-fpm.d/www.conf
#### 默认php.ini：/data/php/conf/php.ini
#### 默认缓存目录：/data/php/tmp/
#### session目录：/data/php/session/


### Nginx相关目录
#### 日志目录：/data/nginx/logs
#### 默认php-fpm.conf：/data/nginx/conf/nginx.conf
#### 默认nginx.conf目录（fastcgi_params文件自行建立）：/data/nginx/conf/
#### 默认*.conf目录：/data/nginx/conf/conf.d/
#### client_temp目录：/data/nginx/tmp/client_temp
#### fastcgi_temp目录：/data/nginx/tmp/fastcgi_temp
#### proxy_temp目录：/data/nginx/tmp/proxy_temp
#### scgi_temp目录：/data/nginx/tmp/scgi_temp
#### uwsgi_temp目录：/data/nginx/tmp/uwsgi_temp



```
### 开放端口：9000 80 443 9001
```


### 启动命令
```
docker run -dit --net host -p 80:80 -p 443:443 -v /data/htdocs:/data/htdocs -v /data/nginx-php/nginx/:/data/nginx/ -v /data/nginx-php/php/:/data/php/ docker.io/w303972870/openresty-php
```


#### 我的配置/data/nginx-php目录结构

```
/data/nginx-php/
├── nginx
│   ├── conf
│   │   ├── cert         这个目录是我用于放https证书的
│   │   │   ├── hc.key
│   │   │   └── hc.pem
│   │   ├── include
│   │   │   └── localhost.conf
│   │   └── nginx.conf
│   ├── logs
│   └── tmp
│       ├── client_temp
│       ├── fastcgi_temp
│       ├── proxy_temp
│       ├── scgi_temp
│       └── uwsgi_temp
└── php
    ├── conf
    │   ├── php-fpm.conf
    │   ├── php-fpm.d
    │   │   └── www.conf
    │   └── php.ini
    ├── logs
    ├── session
    └── tmp
```



		**已安装和支持模块扩展**
```
[PHP Modules]
amqp
bcmath
bz2
Core
ctype
curl
date
dba
dom
enchant
event
exif
fileinfo
filter
ftp
gd
gettext
gmp
hash
iconv
**imagick**
intl
json
ldap
libxml
mbstring
mcrypt
**memcached**
**mongodb**
mysqli
mysqlnd
openssl
pcntl
pcre
PDO
pdo_mysql
pdo_sqlite
Phar
posix
readline
**redis**
Reflection
session
shmop
soap
sockets
sodium
SPL
sqlite3
standard
sysvsem
tokenizer
wddx
xml
xmlreader
xmlrpc
xmlwriter
xsl
yaml
Zend OPcache
zip
zlib
zmq

[Zend Modules]
Zend OPcache
```

		**默认的php.ini文件**
```
[PHP]
engine = On
short_open_tag = On
precision = 14
output_buffering = 4096
zlib.output_compression = Off
implicit_flush = Off
unserialize_callback_func =
serialize_precision = -1
disable_functions =
disable_classes =
zend.enable_gc = On
expose_php = On
max_execution_time = 40
max_input_time = 60
memory_limit = 128M
error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT
display_errors = Off
display_startup_errors = Off
log_errors = On
log_errors_max_len = 1024
ignore_repeated_errors = Off
ignore_repeated_source = Off
report_memleaks = On
html_errors = On
error_log = /data/php/logs/php_errors.log
variables_order = "GPCS"
request_order = "GP"
register_argc_argv = Off
auto_globals_jit = On
post_max_size = 100M
auto_prepend_file =
auto_append_file =
default_mimetype = "text/html"
default_charset = "UTF-8"
include_path = ".:/usr/share/php7"
doc_root =
user_dir =
enable_dl = Off
file_uploads = On
upload_max_filesize = 50M
max_file_uploads = 200
allow_url_fopen = On
allow_url_include = Off
default_socket_timeout = 60
[CLI Server]
cli_server.color = On
[Date]
date.timezone = Asia/Shanghai
[filter]
[iconv]
[intl]
[sqlite3]
[Pcre]
[Pdo]
[Pdo_mysql]
pdo_mysql.cache_size = 2000
pdo_mysql.default_socket=
[Phar]
[mail function]
SMTP = localhost
smtp_port = 25
mail.add_x_header = Off
[ODBC]
odbc.allow_persistent = On
odbc.check_persistent = On
odbc.max_persistent = -1
odbc.max_links = -1
odbc.defaultlrl = 4096
odbc.defaultbinmode = 1
[Interbase]
ibase.allow_persistent = 1
ibase.max_persistent = -1
ibase.max_links = -1
ibase.timestampformat = "%Y-%m-%d %H:%M:%S"
ibase.dateformat = "%Y-%m-%d"
ibase.timeformat = "%H:%M:%S"
[MySQLi]
mysqli.max_persistent = -1
mysqli.allow_persistent = On
mysqli.max_links = -1
mysqli.cache_size = 2000
mysqli.default_port = 3306
mysqli.default_socket =
mysqli.default_host =
mysqli.default_user =
mysqli.default_pw =
mysqli.reconnect = Off
[mysqlnd]
mysqlnd.collect_statistics = On
mysqlnd.collect_memory_statistics = Off
[OCI8]
[PostgreSQL]
pgsql.allow_persistent = On
pgsql.auto_reset_persistent = Off
pgsql.max_persistent = -1
pgsql.max_links = -1
pgsql.ignore_notice = 0
pgsql.log_notice = 0
[bcmath]
bcmath.scale = 0
[browscap]
[Session]
session.save_handler = files
session.use_strict_mode = 0
session.use_cookies = 1
session.use_only_cookies = 1
session.name = PHPSESSID
session.auto_start = 0
session.cookie_lifetime = 0
session.cookie_path = /data/php/session/
session.cookie_domain =
session.cookie_httponly =
session.serialize_handler = php
session.gc_probability = 1
session.gc_divisor = 1000
session.gc_maxlifetime = 1440
session.referer_check =
session.cache_limiter = nocache
session.cache_expire = 180
session.use_trans_sid = 0
session.sid_length = 26
session.trans_sid_tags = "a=href,area=href,frame=src,form="
session.sid_bits_per_character = 5
[Assertion]
zend.assertions = -1
[COM]
[mbstring]
[gd]
[exif]
[Tidy]
tidy.clean_output = Off
[soap]
soap.wsdl_cache_enabled=1
soap.wsdl_cache_dir="/data/php/tmp"
soap.wsdl_cache_ttl=86400
soap.wsdl_cache_limit = 5
[sysvshm]
[ldap]
ldap.max_links = -1
[dba]
[opcache]
opcache.enable_cli=1
opcache.file_cache=/data/php/tmp/
[curl]
[openssl]
```

		**默认的php-fpm.conf**

```
[global]
pid = /data/php/conf/php-fpm7.pid
error_log = /data/php/logs/error.log
daemonize = no
include=/data/php/conf/php-fpm.d/*.conf

```


		**默认的php-fpm.d/wwww.conf**

```
[www]
user = nobody
group = nobody
listen = /dev/shm/php.sock
listen.owner = nobody
listen.group = nobody
listen.mode = 0660
pm = dynamic
pm.max_children = 36 
pm.start_servers = 12
pm.min_spare_servers = 12
pm.max_spare_servers = 24

```

		**默认的nginx.conf**

```
worker_processes 2;
worker_cpu_affinity auto;
worker_rlimit_nofile 65530;
error_log  /data/nginx/logs/nginx_error.log  crit;

events
{
  use epoll;
  worker_connections 65530;
}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile on;
    tcp_nopush on;
    keepalive_timeout 60;
    tcp_nodelay on;
    server_tokens off;
    server_names_hash_bucket_size 128;
    client_header_buffer_size 32k;
    large_client_header_buffers 4 32k;
    client_max_body_size 8m;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for" "$request_time"';

    log_format  post  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for" "$request_time" "$request_body"';

    access_log  /data/nginx/logs/access.log  main;


    gzip  on;
    gzip_min_length 1k;
    gzip_buffers 16 64k;
    gzip_http_version 1.1;
    gzip_comp_level 6;
    gzip_types text/plain application/x-javascript text/css application/xml;
    gzip_vary on;

    limit_req_zone $binary_remote_addr zone=one:3m rate=1r/s;
    limit_req_zone $binary_remote_addr $uri zone=two:3m rate=1r/s;
    limit_req_zone $binary_remote_addr $request_uri zone=thre:3m rate=1r/s;
    include /data/nginx/conf/conf.d/*.conf;
}

```

		**默认的default.conf**

```
server {
    listen 80;
    server_name  localhost;
    root "/data/htdocs";
    index index.html index.htm index.php;

    charset utf-8;

    add_header Strict-Transport-Security max-age=63072000;
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;

    gzip on;
    gzip_min_length 1k;
    gzip_comp_level 2;
    gzip_types application/json text/plain application/javascript application/x-javascript text/css application/xml text/javascript application/x-httpd-php image/jpeg image/gif image/png;
    gzip_vary on;

    if  ( $uri ~* "^/favicon\.ico" ) {
        break;
    }

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    access_log /data/nginx/logs/localhost-access.log main;
    error_log  /data/nginx/logs/localhost-error.log error;

    sendfile off;

    client_max_body_size 100m;

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/dev/shm/php.sock;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        fastcgi_param DOCUMENT_ROOT $realpath_root;
        fastcgi_intercept_errors off;
        fastcgi_buffer_size 16k;
        fastcgi_buffers 4 16k;
        fastcgi_connect_timeout 300;
        fastcgi_send_timeout 300;
        fastcgi_read_timeout 300;
    }

    location ~ /\.ht {
        deny all;
    }
}



```


		**默认的supervisord.conf（';'前必须有一个空格的）**

```
[inet_http_server]
port=127.0.0.1:9001
username=root
password=123456

[supervisord]
nodaemon=true
logfile=/data/supervisor/logs/supervisord.log ; 
pidfile=/data/supervisor/supervisord.pid ; 
childlogdir=/data/supervisor/logs ;

[program:php-fpm]
command=/usr/bin/php-fpm -c /data/php/conf/php.ini -y /data/php/conf/php-fpm.conf --nodaemonize
stopsignal=QUIT
autostart=true ;
autorestart=true ;


[program:nginx]
command=/usr/sbin/nginx -c /data/nginx/conf/nginx.conf -g "daemon off;"
stopsignal=QUIT


```