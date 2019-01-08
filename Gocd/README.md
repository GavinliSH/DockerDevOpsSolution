# docker for SEE
## Preparation
### gocd-server
* file/keys - ssh keys for git,将秘钥对公司要放在当前目录
* packages/plugins - gocd server plugins,将下载的[Good plugins](https://www.gocd.org/plugins/)放在当前目录
### gocd-agent-see
* file/keys - ssh keys for git,将秘钥对公司要放在当前目录
* packages - 环境依赖安装包
    * 将jdk安装包放在当前目录中
        * eg. jdk-8u191-linux-x64.tar.gz
    * 将pmd安装包放在当前目录中
        * eg. pmd-bin-6.4.0.zip
    * 将Python安装包放在当前目录中
        * eg. Python-3.7.1.tgz
    * 将node安装包放在当前目录中
        * eg. node-v8.9.4-linux-x64.tar.xz
## docker compose
运行Gocd server&agent
```
docker-compose up
```
停止Gocd server&agent
```
docker-compose stop
```
启动Gocd server&agent
```
docker-compose start
```
删除Gocd server&agent
```
docker-compose down
```
