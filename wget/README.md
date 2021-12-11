# wget

Docker container definition for wget

Use this container as a sub-container for e.g. scheduler. It uses following environment variables:

```
url=https://google.com
contentOut=wget.txt
requestLog=wget.log
```

The logs-Volume will be used to store the log files.

Include it as a sub-container in a docker compose yaml like this:

```yaml
wget-google:
  build:
    context: ../wget/
    dockerfile: Dockerfile
  container_name: wget-google
  environment:
    - url=https://google.com
    - contentOut=wget.txt
    - requestLog=wget.log
  volumes:
      - ../wget/logs:/logs:rw
```

