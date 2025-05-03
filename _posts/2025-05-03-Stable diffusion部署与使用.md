---
layout: post
title: Stable diffusion部署与使用
tags:
- AI绘图
- stable diffusion
categories: AI绘图
description: 
---

### 1. 安装homebrew

` /bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/homebrew-install/raw/master/install.sh)”`

---

### 2.安装 stable diffusion webui 的依赖

`brew install cmake protobuf rust python@3.10 wget`

---


### 3. Pip设置镜像

`pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/`

若设置pip config的时候遇到**permission**的问题，可以对其上级文件夹`sudo chmod -R 777` 文件夹路径，使得pip config可以设置成功

### 4. 下载 stable diffusion webui 代码

```cd
git clone https://gitee.com/ineo6/stable-diffusion-webui.git
```

### 5. 启动 stable diffusion webui 本体

`cd ~/stable-diffusion-webui ./webui.sh`

在启动的过程中需要从github中拉取一些组件，需要切换github的加速源，一般选择自营加速源：

`/bin/bash -c "$(curl -fsSL https://gitee.com/ineo6/stable-diffusion-webui/raw/master/super-gh.sh)”`

```
1) ghproxy.com      3) ghps.cc               5)hub.gitmirror.com
2) 自营加速源          4) gh.ddlc.top        6) gh.con.sh
 #?
```

另外找到stable diffusion webui的工程文件夹，找到**modules/launch_utils.py**的文件，给github组件的路径前添加`ghproxy.com/`，示例如下：

![ghproxy.com/](_data/post_img/2025-05-03-Stable_diffusion/ghproxy.jpeg "ghproxy.com/")

若报错**Can't load tokenizer for ‘openai/clip-vit-large-patch14’**，则是因为其从huggingface拉取失败，可以自行下载并放置到*stable-diffusion-webui/openai/clip-vit-large-patch14*，这样处理完就可以启动成功了。

若出现Running on local URL:  http://127.0.0.1:7860并弹出界面，则启动成功了。