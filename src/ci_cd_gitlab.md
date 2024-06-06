---
layout: lecture
title: "CICD in Gitlab"
date: 2022-04-21
ready: true
---

### Step 1
Add `.gitlab-ci.yml` in the root folder of the project

```yaml
# .gitlab-ci.yml
before_script:
  - python --version
  - pip install -r requirements.txt
​
stages:
  - build
  - test
  - deploy
​
build_job:
  stage: build # 指定job所属stage
  image: centos:7 # 指定执行job的所使用docker镜像
  tags: 
    - ci_test # 指定执行job的runner（即机器）
  script: # job执行时运行的脚本
    - echo "build project"
​
test_job:
  stage: test
  image: centos:7
  tags: 
    - ci_test
  script:
    - echo "test project"
​
deploy_job:
  stage: deploy
  image: centos:7
  tags: 
    - ci_test
  script:
    - echo "deploy project"
```

### Step2

Start GitLab runner

[https://docs.gitlab.com/runner/install/linux-manually.html](https://docs.gitlab.com/runner/install/linux-manually.html)

```shell
wget https://gitlab-runner-downloads.s3.amazonaws.com/latest/deb/gitlab-runner_amd64.deb
sudo dpkg -i gitlab-runner_amd64.deb
sudo gitlab-runner start
```

### Step3

Register GitLab runner

```shell
sudo gitlab-runner register
```

Check whether there is any runner in Setting -> CI/CD -> Runners

![](https://raw.githubusercontent.com/Yukun4119/BlogImg/main/ubuntu\_img/20220429170510.png)

### Step4

After `git push`, CICD will be executed automatically.

![](https://raw.githubusercontent.com/Yukun4119/BlogImg/main/ubuntu\_img/20220429170737.png)

In `Pipelines`, we can get the status of each stage.

![](https://raw.githubusercontent.com/Yukun4119/BlogImg/main/ubuntu\_img/20220429170813.png)

In `Jobs`, we can get the log of execution history

![](https://raw.githubusercontent.com/Yukun4119/BlogImg/main/ubuntu\_img/20220429170934.png)

### References

[https://www.youtube.com/watch?v=jUiKi6FWYrg](https://www.youtube.com/watch?v=jUiKi6FWYrg)

[https://docs.gitlab.com/ee/ci/](https://docs.gitlab.com/ee/ci/)

[https://docs.gitlab.com/runner/](https://docs.gitlab.com/runner/)

[http://www.yamllint.com/](http://www.yamllint.com/)

[https://juejin.cn/post/7002764771330097189](https://juejin.cn/post/7002764771330097189)

## Set up CICD for Python Program

### Step 1 Set up gitlab-Runner

```shell
docker pull gitlab/gitlab-runner:latest
​
docker run -d --name gitlab-runner --restart always -p 8093:8093 -v /var/run/docker.sock:/var/run/docker.sock -v gitlab-runner-config:/etc/gitlab-runner gitlab/gitlab-runner:latest
​
docker exec -it gitlab-runner gitlab-runner register
# Choose Shell in the last step
```

### Step 2 Set up SSH

```shell
docker exec -it gitlab-runner bash
su gitlab-runner
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub username@ip
```

### Step 3 .gitlab-ci.yml

```yaml
stages:
  - clean_env
  - deploy_src
  - install_dependency
  - restart_server
​
variables:
  BASE_DIR: "/test/"
​
job clean_env_job:
  stage: clean_env
  script:
    - ssh -o StrictHostKeyChecking=no ryan@23.105.209.XXX -p 30359 ls
    - ssh -o StrictHostKeyChecking=no ryan@23.105.209.XXX -p 30359 rm -rf judeai
    - ssh -o StrictHostKeyChecking=no ryan@23.105.209.XXX -p 30359 tmux kill-session -t jude
  tags:
    - Jude
  only:
    - main
  when: always
​
​
job deploy_src_job:
  stage: deploy_src
  script:
    # 复制新的项目到生产机器
    - ssh -o StrictHostKeyChecking=no -p 30359 ryan@23.105.209.XXX git clone https://gitlab.com/Y.K.Shang/judeai.git
  tags:
    - Jude
  only:
    - main
  when: always
​
​
job install_dependency_job:
  stage: install_dependency
  script:
    # 安装环境所需要的依赖
    - ssh -o stricthostkeychecking=no ryan@23.105.209.XXX -p 30359  pip install -r judeai/requirements.txt
  tags:
    - Jude
  only:
    - main
  when: manual
​
​
job restart_server_job:
  stage: restart_server
  script:
    - ssh -o Stricthostkeychecking=no ryan@23.105.209.XXX -p 30359 tmux new -s jude -d
    - ssh -o StrictHostKeyChecking=no ryan@23.105.209.XXX -p 30359 tmux send -t jude "python3\ judeai/run.py" C-m
  tags:
    - Jude
  only:
    - main
  when: always
```

\
