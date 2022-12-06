# kubernetes-LEMP-sample

This repo is providing a simple manifest that constract LEMP on kubernetes.

# configuration 
- line 6    - 16   is a statement about www data. No changes to be made.
- line 18   - 118  is a statement about database. The username, password, and root password for lines 37 to 45 need to be changed.  
  ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
    name: mariadb
  type: Opaque
  data:
    ## 
    # @WARNING: THIS IS SAMPLE CONFIGURATION.
    # username: maria
    # password: pASsW0rD
    # rtpasswd: pASsW0rD     (root password)
    ## 
    username: bWFyaWE=
    password: cEFTc1cwckQ=
    rtpasswd: cEFTc1cwckQ=
  ```
- line 120  - 2144 is a statement about php.      In some cases, change php.ini from line127 to 2084.
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: php
  data:
    php.ini: |
      [PHP]
    
      ;;;;;;;;;;;;;;;;;;;
      ; About php.ini   ;
      ;;;;;;;;;;;;;;;;;;;
      
      ・・・
      
      ;ffi.preload=
  ```
- line 2146 - 2230 is a statement about nginx.    In some cases, change php.ini from line2153 to 2170.
  ```yaml
  apiVersion: v1
  kind: ConfigMap
  metadata:
    name: nginx
  data:
    default.conf: |
      server {
        listen 80;
        server_name _;
        root /var/www/html;
        index index.php index.html;
        location / {
          try_files $uri $uri/ /index.php$is_args$args;
        }
        location ~ [^/]\.php(/|$) {
          fastcgi_split_path_info ^(.+?\.php)(/.*)$;
          fastcgi_pass php:9000;
          fastcgi_index index.php;
          include fastcgi_params;
          fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
          fastcgi_param PATH_INFO $fastcgi_path_info;
        }
      }
  ```

# test
```sh
#!/bin/bash
# For those building on a trial basis
NAMESPACE=lemp
kubectl create namespace $NAMESPACE
kubectl -n lemp apply -f https://raw.githubusercontent.com/ES-Yukun/kubernetes-LEMP-sample/main/lemp.yaml
```
