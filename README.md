# Uptime Kuma Docker Build via GitHub Actions

此仓库利用 GitHub Actions 自动构建和推送 [Uptime Kuma](https://github.com/louislam/uptime-kuma) 的 Docker 镜像。

## 目录

- [简介](#简介)
- [功能](#功能)
- [使用方法](#使用方法)
- [工作流程](#工作流程)

## 简介

本项目通过 GitHub Actions 定时构建和更新 Uptime Kuma 的 Docker 镜像，并推送到 Docker Hub。

## 功能

- 定时构建 Docker 镜像
- 推送镜像到 Docker Hub
- 构建成功或失败时发送钉钉通知

## 使用方法

1. **Fork 此仓库**
2. **配置 GitHub Secrets 和 Variables**

   为了推送 Docker 镜像并发送通知，需要配置以下 GitHub Secrets 和 Variables：

   | 名称                        | 描述                         |
   |-----------------------------|------------------------------|
   | `secrets.DOCKERHUB_TOKEN`   | Docker Hub 的访问令牌       |
   | `vars.DOCKERHUB_USERNAME`   | 你的 Docker Hub 用户名       |
   | `secrets.DINGTALK_SECRET`   | 钉钉机器人的密钥            |
   | `secrets.DINGTALK_ACCESS_TOKEN` | 钉钉机器人的访问令牌     |

3. **触发构建**

   工作流程会在每天的凌晨 0:00（中国时间早上 8:00）自动运行，或者可以手动触发。

## 工作流程

GitHub Actions 工作流程文件位于 `.github/workflows/uptime-kuma-Build-and-Push-Docker-Image.yml`，其主要步骤包括：

1. **设置仓库** - 克隆 Uptime Kuma 源代码。
2. **设置 Docker Buildx** - 准备 Docker 构建环境。
3. **登录 Docker Hub** - 使用 Docker Hub 凭证登录。
4. **创建 Dockerfile** - 动态生成 Dockerfile。
5. **构建并推送镜像** - 构建 Docker 镜像并推送到 Docker Hub。
6. **发送钉钉通知** - 构建成功或失败时发送通知。
