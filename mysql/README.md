# MySQL with debug

This images are based on [the official image](https://github.com/docker-library/mysql).

Usage can refer to [how-to-remote-debug-on-macos](https://github.com/y-asaba/docker-mysql-debug#how-to-remote-debug-on-macos)


## Examples

`docker-compose.yaml`

```yaml
version: "3.0"
services:
  mysql80-debug:
    image: wdeil/mysql:8.0.26-debug
    cap_add:
      - SYS_PTRACE
    security_opt:
      - seccomp:unconfined
    ports:
      - 3306:3306
      - 33060:33060
      - 2345:2345
    environment:
      MYSQL_ROOT_PASSWORD: <your_root_password>
    restart: unless-stopped
    container_name: mysql80-debug
```

Or

```bash
docker run -e MYSQL_ROOT_PASSWORD=<your_root_password> -p 2345:2345 -p 3306:3306 --cap-add=SYS_PTRACE --security-opt seccomp=unconfined --rm wdeil/mysql:8.0.26-debug
```

More information of environment variables can refer to [https://dev.mysql.com/doc/refman/5.7/en/environment-variables.html](https://dev.mysql.com/doc/refman/5.7/en/environment-variables.html)





