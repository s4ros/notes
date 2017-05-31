# Linux shell tips&tricks

## 100% Inodes usage issue

```shell
# Try to find places where you have tons of files.
find / -xdev -printf '%h\n' | sort | uniq -c | sort -k 1 -n
```

## remove Docker old images and containers

```shell
# remove containers
docker rm $(docker ps --no-trunc -aq)

# remove images
docker rmi $(docker images -q)
```
