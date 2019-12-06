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

    Supported variables: [defaults/proxy.yml](defaults/proxy.yml).

  * `fastcgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx fastcgi module settings](http://nginx.org/ru/docs/http/ngx_http_fastcgi_module.html).
    
    If passed virtual hosts does not contains fastcgi-type host values of `fastcgi_params` module will be setted to minimum possible values.

    Supported variables: [defaults/fastcgi.yml](defaults/fastcgi.yml).

  * `uwsgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx uwsgi module settings](https://nginx.org/ru/docs/http/ngx_http_uwsgi_module.html).

    If passed virtual hosts does not contains uwsgi-type host values of `uwsgi_params` module will be setted to minimum possible values.

    Supported variables: [defaults/uwsgi.yml](defaults/uwsgi.yml).

  * `scgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx scgi module settings](http://nginx.org/en/docs/http/ngx_http_scgi_module.html).

    If passed virtual hosts does not contains scgi-type host values of `scgi_params` module will be setted to minimum possible values.

    Supported variables: [defaults/scgi.yml](defaults/scgi.yml).

  * `gzip_params: dict`
    Params for gzip settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx gzip module settings](https://nginx.org/ru/docs/http/ngx_http_gzip_module.html).

    Supported variables: [defaults/gzip.yml](defaults/gzip.yml).

  * `logs_params: dict`
    Params for logs settings like `log_format`, `access_log` and etc. This is variable for [Nginx logs module settings](https://nginx.org/ru/docs/http/ngx_http_log_module.html).

    Supported variables: [defaults/logs.yml](defaults/logs.yml).

  * `ssl_params: dict`
    Params for gzip settings like `ssl_buffer_size`, `ssl_ciphers` and etc. This is variable for [Nginx ssl module settings](https://nginx.org/ru/docs/http/ngx_http_ssl_module.html).

    Supported variables: [defaults/ssl.yml](defaults/ssl.yml).

Dependencies
------------

  * gudron.nginx_vhost - [Role-generator of nginx virtual host config files](https://github.com/gudron/gudron.nginx_vhost)

Example Playbook
----------------

  - hosts: example_project:&example_project_stage
    any_errors_fatal: "{{ any_errors_fatal | default(true) }}"
    gather_facts: false
    vars:
      ansible_connection: local
      ansible_become: no
      ansible_distribution: Debian
          
    roles:
      - name: gudron.nginx_config
        vars: 
          conf_file_path: /any/path/to/nginx/config/files/directory/
          virtual_hosts_destintion_path: /example/project/nginx/conf.d/sites-available/
          proxy_params:
            http_version: "1.0"
            buffering: "on"
            buffers_count: 4
            buffer_size: 256k
            buffer_size_first_response: 512k
            busy_buffers_size: 512k
            connect_timeout: 30s
            read_timeout: 31s
          virlual_hosts_params:
            api:
              port: 80
              domain: api.example.com
              type: proxy
              root: /example/project/app/static/dir/
              status_path: ngxstatus
              headers:
                X-Content-Type-Options: nosniff
                Strict-Transport-Security: max-age=31536000; includeSubDomains
                X-Frame-Options: SAMEORIGIN
              proxy_params:
                X-Real-IP: $remote_addr
              include_params:
                - /etc/nginx/conf.d/include_file.conf
              backends: 
                - address: api.example.internal
                  port: 8080


License
-------

BSD
