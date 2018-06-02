# makehost
<h2>Bash script for creating/deleting NGINX local hosts for Mac OSX</h2>

There is <b>makehost</b> bashscript. Easiest way to create and delete localhosts for NGINX. This version had been writing for MacOS X. You can fork and write version for your OS. 

## Installation ##

1. Download the script
2. Apply permission to execute:

```bash
$ chmod +x /path/to/makehost
```

3. Copy the file to your /usr/local/bin directory:

```bash
$ sudo cp /path/to/makehost /usr/local/bin/makehost
```

## Usage ##

```bash
$ sudo makehost [add | delete] [domain] [optional host_dir]
```

### Examples ###

to create a new virtual host:

```bash
$ sudo makehost add mysite.loc
```
to create a new virtual host with custom directory name:

```bash
$ sudo makehost add mysite.loc my_dir
```
to delete a virtual host

```bash
$ sudo makehost delete mysite.loc
```

to delete a virtual host with custom directory name:

```
$ sudo makehost delete mysite.loc my_dir
```


<h2>My configs</h2>

<b>/usr/local/etc/nginx/nginx.conf</b>
<pre><code>
worker_processes  1;

error_log  /usr/local/var/log/nginx/error.log;

events {
    worker_connections  1024;
}

http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$re$
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /usr/local/var/log/nginx/access.log  main;

    sendfile        on;

    keepalive_timeout  65;

    index index.html index.php;

    upstream www-upstream-pool{
        server unix:/tmp/php-fpm.sock;
    }

    include /etc/nginx/conf.d/*.conf;
    include /usr/local/etc/nginx/sites-enabled/*.conf;
}
</code></pre>

<b>/private/etc/hosts</b>
<pre><code>
127.0.0.1       localhost       *.loc
255.255.255.255 broadcasthost
::1             localhost
</code></pre>

