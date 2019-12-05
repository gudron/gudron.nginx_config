gudron.nginx_conf
=========

Role-generator of nginx config files and [proxy role](https://github.com/gudron/gudron.nginx_vhost) for create virtual hosts config files.

Role Variables
--------------

### General variables

  * `client: dict`
    Set client settings like `max_body_size`, `body_timeout` and etc.

  * `fastcgi_params: dict`
    Params for fastcgi settings like `buffers_count`, `buffer_size` and etc. This is variable for [Nginx fastcgi module settings](http://nginx.org/ru/docs/http/ngx_http_fastcgi_module.html)

Dependencies
------------

  * gudron.nginx_vhost - [Role-generator of nginx virtual host config files](https://github.com/gudron/gudron.nginx_vhost)

Example Playbook
----------------


License
-------

BSD
