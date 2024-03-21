
# Домашние задания по модулю  «Отказоустойчивость»

В этом репозитории расположены ваши домашние задания к каждой лекции. 

Обязательны к выполнению задачи без звездочек. Их нужно выполнить, чтобы получить зачёт.

Задачи со звёздочкой (*) — дополнительные задачи или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Любые вопросы по решению задач задавайте в чате учебной группы. Ссылку вы найдёте в письме на вашей электронной почте.
=======
# Домашнее задание к занятию "Отказоустойчивость в облаке" - Лапшов Сергей
=======
### Задание 1

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
global
    log /dev/log        local0
    log /dev/log        local1 notice
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
    stats timeout 30s
    user haproxy
    group haproxy
    daemon

    # Default SSL material locations
    ca-base /etc/ssl/certs
    crt-base /etc/ssl/private

    # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermediate
    ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
    ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
    ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets

defaults
    log         global
    mode        http
    option      httplog
    option      dontlognull
    timeout connect 5000
    timeout client  50000
    timeout server  50000
    errorfile 400 /etc/haproxy/errors/400.http
    errorfile 403 /etc/haproxy/errors/403.http
    errorfile 408 /etc/haproxy/errors/408.http
    errorfile 500 /etc/haproxy/errors/500.http
    errorfile 502 /etc/haproxy/errors/502.http
    errorfile 503 /etc/haproxy/errors/503.http
    errorfile 504 /etc/haproxy/errors/504.http

listen stats  # веб-страница со статистикой
    bind                    :888 # Исправлено порт
    mode                    http
    stats                   enable
    stats uri               /stats
    stats refresh           5s
    stats realm             Haproxy\ Statistics

frontend example  # секция фронтенд
    mode http
    bind :8088
    default_backend web_servers
    acl ACL_example.com hdr(host) -i example.com
    use_backend web_servers if ACL_example.com

backend web_servers    # секция бэкенд
    mode http
    balance roundrobin
    option httpchk
    http-check send meth GET uri /index.html
    server s1 127.0.0.1:8888 check
    server s2 127.0.0.1:9999 check
    server s3 127.0.0.1:10000 check
    server s4 127.0.0.1:10001 check

listen web_tcp
    bind :1325
    
    server s1 127.0.0.1:8888 check inter 3s
    server s2 127.0.0.1:9999 check inter 3s
```

`При необходимости прикрепитe сюда скриншоты
![скриншоты, где видно перенаправление запросов на разные серверы при обращении к HAProxy.](https://github.com/DavyRoy/sflt-homeworks_8-03/blob/main/Снимок%20экрана%20от%202024-03-21%2011-02-36.png)
---

### Задание 2

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
global
    log /dev/log        local0
    log /dev/log        local1 notice
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
    stats timeout 30s
    user haproxy
    group haproxy
    daemon

    # Default SSL material locations
    ca-base /etc/ssl/certs
    crt-base /etc/ssl/private

    # See: https://ssl-config.mozilla.org/#server=haproxy&server-version=2.0.3&config=intermediate
    ssl-default-bind-ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384
    ssl-default-bind-ciphersuites TLS_AES_128_GCM_SHA256:TLS_AES_256_GCM_SHA384:TLS_CHACHA20_POLY1305_SHA256
    ssl-default-bind-options ssl-min-ver TLSv1.2 no-tls-tickets

defaults
    log         global
    mode        http
    option      httplog
    option      dontlognull
    timeout connect 5000
    timeout client  50000
    timeout server  50000
    errorfile 400 /etc/haproxy/errors/400.http
    errorfile 403 /etc/haproxy/errors/403.http
    errorfile 408 /etc/haproxy/errors/408.http
    errorfile 500 /etc/haproxy/errors/500.http
    errorfile 502 /etc/haproxy/errors/502.http
    errorfile 503 /etc/haproxy/errors/503.http
    errorfile 504 /etc/haproxy/errors/504.http

listen stats  # веб-страница со статистикой
    bind                    :888 # Исправлено порт
    mode                    http
    stats                   enable
    stats uri               /stats
    stats refresh           5s
    stats realm             Haproxy\ Statistics

frontend example  # секция фронтенд
    mode http
    bind :8088
    default_backend web_servers
    acl example_domain hdr(host) -i example.local
    use_backend web_servers if example_domain

backend web_servers    # секция бэкенд
    mode http
    balance roundrobin
    option httpchk
    http-check send meth GET uri /index.html
    server s1 127.0.0.1:8888 weight 2 check
    server s2 127.0.0.1:9999 weight 3 check
    server s3 127.0.0.1:10010 weight 4 check
    server s4 127.0.0.1:10000 check
    server s5 127.0.0.1:10001 check

listen web_tcp
    bind :1325
    
    server s1 127.0.0.1:8888 check inter 3s
    server s2 127.0.0.1:9999 check inter 3s
```

`При необходимости прикрепитe сюда скриншоты
![перенаправление запросов на разные серверы при обращении к HAProxy c использованием домена example.local и без него](https://github.com/DavyRoy/sflt-homeworks_8-03/blob/main/Снимок%20экрана%20от%202024-03-21%2011-34-38.png)


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
>>>>>>> 73d1e2b (commit)
