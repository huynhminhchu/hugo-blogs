---
title: Deploy Gitlab on Virtual Machines
date: 2023-03-05T09:29:33Z
featured: false
draft: false
comment: true
toc: true
reward: true
pinned: false
carousel: false
series: [Gitlab]
categories: [Deployment]
tags: []
images: []
---

Summary.

<!--more-->

# Prerequisite
- Ubuntu Server 20.04 LTS

# Install and configure the necessary dependencies
```
    sudo apt-get update -y
    sudo apt-get install -y curl openssh-server ca-certificates tzdata perl
    sudo apt-get install -y postfix
```
# Add the GitLab package repository and install the package
```
    curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ee/script.deb.sh | sudo bash
    sudo EXTERNAL_URL="https://gitlab.chuhuynh.com" apt-get install gitlab-ee
```
