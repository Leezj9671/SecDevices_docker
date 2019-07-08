# Nessus

## 使用

1. 建立image
2. 运行容器，等待插件安装完成即可

```bash
docker build -t test/nessus .
#视情况决定是否使用Volume
docker run -d -m 2048M -v NESSUS_VOL:/opt/nessus -v /usr/share/zoneinfo:/usr/share/zoneinfo:ro -p 8834:8834 --name nessus test/nessus
```

3. 修改密码，默认用户名为 Nessus

```bash
docker exec -it nessus /bin/bash
/opt/nessus/sbin/nessuscli chpasswd Nessus
```
