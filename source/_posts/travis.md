title: 通过 Travis CI 部署博客
date: 2020-02-24 22:21:00
desc: 
tags: [DevOps] 
index_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/travis.jpg
banner_img: https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/travis.jpg
---

CI/CD 讲的是软件开发通过软件工程的手段优化开发流程，提高开发质量的一个手段。

<!-- more -->

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/ci_tools.png)

CI/CD 并不是指的某一个工具，但是通常好的 CI/CD 工具都拥有相同的功能。

# 持续集成（Continuous integration）

在我看来，持续集成分为两个方面来看待，其一是集成，就是将代码不断合并到一个大的系统上。然后是持续，持续体现在可能这个代码仓库不断有频繁的贡献，然后得到不断的反馈。在我看来持续集成是一个源码控制的工具。

采用持续集成时，开发人员会定期将代码变更合并到一个中央存储库中，之后系统会自动运行构建和测试操作。持续集成的主要目标是更快发现并解决缺陷，提高软件质量，并减少验证和发布新软件更新所需的时间。

通常，代码的一次 PR 操作会触发一次 CI，CI 会对这次 PR 合并之后的代码做静态检测（包括代码风格、代码规范），进行单元测试，然后进行构建（Build）。

# 持续部署（Continuous Deployment）or 持续交付（Continuous Delivery）

其实讲的大体上应该是一个东西，在代码合并入仓库之后，将二进制文件或者是源代码等部署到测试环境，或者是生产环境。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/jarvis.jpg)

Travis 的取名，会不会和 Jarvis 有几分关系呢？

# 通过 Travis 自动更新 Github Page

https://travis-ci.org/ Travis CI 只支持 Github，不支持其他代码仓库。

登录并授权过后只需要将需要 CI 的 repo 勾上，然后进行进一步配置。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/travis_index.png)

如图所示，我将我的 Github Page 和一个名为 blog-travis 的仓库分开，后者是我使用的基于 Hexo 的源码，每一次 blog-travis repo 的更新都将触发一次 CI job。

![](https://edgsheryl.oss-cn-hangzhou.aliyuncs.com/travis/travis_setting.png)

点击 Setting，我们就能够设置触发条件、定义 CI 脚本的环境变量等。

最后，使用 Travis CI 的关键就在于编写一个执行流程的 YAML 文件，命名为 `.travis.yml`，保存在你项目根目录下。该 YAML 文件指定了环境，执行命令。当然在 CI/CD 阶段我们可能需要打包镜像，或者是使用 Token，密钥，这部分可以通过 Travis CI 的环境变量传入，也可以通过加密文件上传，线上解密的方式传输。

```yaml
language: node_js
os: linux
committer_from_gh: true
node_js:
  - 13.1.0

before_install:
  - npm install -g hexo-cli

# Start: Build Lifecycle
install:
  - npm install
  - npm install hexo-deployer-git --save

script:
  - hexo clean
  - hexo generate

after_script:
  - sed -i "s/gh_token/${GITHUB_TOKEN}/g" ./_config.yml
  - hexo deploy
# End: Build LifeCycle
```

秘诀就在于将环境变量替换成 URL，然后使用这个 Token 更新你的 repo

```yaml
deploy:
  type: git
  repo: https://gh_token@github.com/edgsheryl/edgsheryl.github.io.git
  branch: master
```

在配置完 CI/CD 之后，我每次更新博客只需要更新我的 Markdown 文件，Commit and Push 就能够完成博客的更新了。
