# kubernetes自动化CICD

## DevOps 

软件开发流程包括
- PLAN：开发团队根据客户的目标制定开发计划
- CODE：根据PLAN开始编码过程，需要将不同版本的代码存储在一个库中。
- BUILD：编码完成后，需要将代码构建并且运行。
- TEST：成功构建项目后，需要测试代码是否存在BUG或错误。
- DEPLOY：代码经过手动测试和自动化测试后，认定代码已经准备好部署并且交给运维团队。
- OPERATE：运维团队将代码部署到生产环境中。
- MONITOR：项目部署上线后，需要持续的监控产品。
- INTEGRATE：然后将监控阶段收到的反馈发送回PLAN阶段，整体反复的流程就是DevOps的核心，即持续集成、持续部署。

![](../images/devops01.png)

DevOps 强调的是高效组织团队之间如何通过自动化的工具协作和沟通来完成软件的生命周期管理，从而更快、更频繁地交付更稳定的软件。


## 环境准备

### GitLab 安装

- 启动gitlab 
```
~]# mkdir -pv /data/apps/gitlab/{config,logs,data}
~]# chmod 777 /data/apps/gitlab -R
~]# cd /data/apps/gitlab
~]# cat > docker-compose.yml <<EOF
version: '3.1'
services:
  gitlab:
    image: 'gitlab/gitlab-ce:latest'
    container_name: gitlab
    restart: always
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://192.168.122.250'
        gitlab_rails['gitlab_shell_ssh_port'] = 2224
    ports:
      - '80:80'
      - '2224:2224'
    volumes:
      - './config:/etc/gitlab'
      - './logs:/var/log/gitlab'
      - './data:/var/opt/gitlab'
EOF

gitlab]# docker-compose  up  -d 
```
- 查看初始密码
``` 
docker exec -it gitlab cat /etc/gitlab/initial_root_password
```

### Jenkins 安装

- 安装jdk
``` 
```