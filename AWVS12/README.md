# AWVS

## 简述

1. 因为破解版有些问题，有时候一个星期后虽然仍然显示永久激活，但实际上并不可用，二次激活会出现奇怪的问题……
2. 其它人发的 docker 不是很透明，担心不可控，还是自己写一个吧又不难……
3. 破解版做一下隔离会比较好

因此萌发了用 docker 做扫描器的想法。

## 使用

1. 使用的 AWVS 安装包从  下载
2. 将破解补丁 `patch_awvs` 和安装包 `acunetix_trail.sh` 放在该目录下。安装包可以直接从官网下载，而破解补丁用的是广为流传的、52破解上的破解补丁，如有担心可以更换为自己信任的补丁
3. 运行 Dockerfile
4. 成功运行后需要手动进入容器进行激活，不过也很简便啦
5. 用户名密码：admin@test.com/Aa123456，可在 Dockerfile 自行修改

```bash
#build image
docker build -t test/wvs .

#按需修改
docker run -m 2048M -d -p 13443:13443 --name wvs test/wvs

#进入容器 patch
docker exec -it -u root wvs /bin/bash
#运行
> ./patch_awvs
```

## 已知缺陷

1. 数据库没法做持久化，不知道是我的姿势有误还是什么问题……
    > 解决方法：使用漏洞管控平台对接，如 [SeMF](https://gitee.com/gy071089/SecurityManageFramwork) 啥的
