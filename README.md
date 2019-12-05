gudron.nginx_conf
=========

Role-generator of nginx config files and [proxy role](https://github.com/gudron/gudron.nginx_vhost) for creation virtual hosts config files.

Role Variables
--------------

### General variables

  * `nginx: dict`
    Set main nginx config files settings like `user`, `worker_processes` and etc.

  * `events_params: dict`
    Set event section settings in main nginx config files. Like `worker_connections`, `accept_mutex` and etc.

  * `conf_file_path: string`
    Nginx config directory path. In this directory will be rendered server config files. Path like that - /any/path/to/nginx/config/files/directory/

  * `virlual_hosts_params: dict`
    Dict of virtual hosts parameters. https://github.com/gudron/gudron.nginx_vhostLike `type`, `domain`, `chartset` and etc. That setting will be proxied to [gudron.nginx_vhost](https://github.com/gudron/gudron.nginx_vhost) dependent role.

  * `client: dict`
    Set client settings like `max_body_size`, `body_timeout` and etc.

  * `common: dict`
    Set common settings like `sendfile`, `server_tokens`, `keepalive_timeout` and etc.

  * `proxy_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx proxy module settings](https://nginx.org/ru/docs/http/ngx_http_proxy_module.html). 
    If passed virtual hosts does not contains proxy-type host values of `proxy_params` module will be setted to minimum possible values.

  * `fastcgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx fastcgi module settings](http://nginx.org/ru/docs/http/ngx_http_fastcgi_module.html)
    If passed virtual hosts does not contains fastcgi-type host values of `fastcgi_params` module will be setted to minimum possible values.

  * `uwsgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx uwsgi module settings](https://nginx.org/ru/docs/http/ngx_http_uwsgi_module.html)
    If passed virtual hosts does not contains uwsgi-type host values of `uwsgi_params` module will be setted to minimum possible values.

  * `scgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx scgi module settings](http://nginx.org/en/docs/http/ngx_http_scgi_module.html)
    If passed virtual hosts does not contains scgi-type host values of `scgi_params` module will be setted to minimum possible values.

  * `gzip_params: dict`
    Params for gzip settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx gzip module settings](https://nginx.org/ru/docs/http/ngx_http_gzip_module.html)

  * `logs_params: dict`
    Params for logs settings like `log_format`, `access_log` and etc. This is variable for [Nginx logs module settings](https://nginx.org/ru/docs/http/ngx_http_log_module.html)

  * `ssl_params: dict`
    Params for gzip settings like `ssl_buffer_size`, `ssl_ciphers` and etc. This is variable for [Nginx ssl module settings](https://nginx.org/ru/docs/http/ngx_http_ssl_module.html)

Dependencies
------------

  * gudron.nginx_vhost - [Role-generator of nginx virtual host config files](https://github.com/gudron/gudron.nginx_vhost)

Example Playbook
----------------


License
-------

BSD
