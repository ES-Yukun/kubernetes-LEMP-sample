# kubernetes-LEMP-sample

This repo is providing a simple manifest that constract LEMP on kubernetes.

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
    # password: pASsW0rD#
    # rtpasswd: pASsW0rD#     (root password)
    ## 
    username: bWFyaWEK
    password: cEFTc1cwckQjCg==
    rtpasswd: cEFTc1cwckQjCg==
  ```
- line 120  - 2144 is a statement about php.      In some cases, change php.ini from line127 to 2084.  
- line 2146 - 2230 is a statement about nginx.    In some cases, change php.ini from line2153 to 2170.  

```sh
#!/bin/bash
# For those building on a trial basis
NAMESPACE=lemp
kubectl create namespace $NAMESPACE
kubectl -n lemp apply -f https://raw.githubusercontent.com/ES-Yukun/kubernetes-LEMP-sample/main/lemp.yaml
```
