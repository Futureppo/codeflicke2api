# CodeFlicker2API

## 注意！！
目前官方风控加强，反代就封号，请仔细考虑后再使用本项目！！

> [!CAUTION]
> **免责声明**
>
> 本项目仅供学习研究和技术交流使用，**严禁用于任何商业用途或非法活动**。
>
> - 本项目通过逆向工程分析 CodeFlicker (KwaiPilot) 的通信协议，将其内部 API 转换为 OpenAI 兼容格式。此行为可能违反 CodeFlicker 的服务条款（ToS）。
> - 使用本项目产生的一切后果（包括但不限于账号封禁、法律纠纷等）由使用者自行承担，项目开发者不承担任何责任。
> - 本项目不提供任何形式的担保，包括但不限于适销性、特定用途适用性和非侵权性的暗示担保。
> - 如收到相关方的合规通知，本项目将立即下架。
>
> **使用本项目即表示您已阅读并同意以上声明。**

## 简介

CodeFlicker2API 是一个将快手 CodeFlicker（KwaiPilot）AI 编码助手的 API 转换为 **OpenAI** 和 **Anthropic** 兼容格式的反向代理服务，内置 Web 管理面板，支持多账号轮询、批量导入与一键 Token 刷新。

## 功能特性

- **双协议兼容** — 同时支持 OpenAI (`/v1/chat/completions`) 和 Anthropic (`/v1/messages`) 接口格式
- **多模型支持** — 自动拉取上游模型列表，支持 GPT、Claude、DeepSeek、Glm、Kimi 等多家模型
- **账号池轮询** — 线程安全的 Round-Robin 调度，自动跳过异常账号
- **自愈机制** — 自动识别限速 / 封禁状态，限速账号 5 分钟后自动恢复
- **批量导入** — 支持 JSON 粘贴或文件上传，自动从 JWT 中提取 UserID
- **一键刷新** — 通过 email/password 批量刷新即将过期的 JWT Token
- **可视化面板** —  内嵌 Web 管理界面，账号管理、Key 管理、系统设置一站式操作
- **Function Calling** — 完整支持 OpenAI Tool Use / Function Calling 能力
- **流式与非流式** — 同时支持 SSE 流式和标准 JSON 两种响应模式

## 快速开始

### 本地运行

```bash
# 编译运行
go build -o codeflicke2api.exe .
./codeflicke2api.exe

# 或直接运行
go run .
```

### Docker 部署

```bash
# Docker Compose（推荐）
docker compose up -d

# 手动构建
docker build -t codeflicke2api .
docker run -d -p 8080:8080 -v ./data:/app/data codeflicke2api
```

启动后访问 `http://localhost:8080`，使用默认 Token `123456` 登录管理面板。

## 项目结构

```
codeflicke2api/
├── main.go              # 入口，路由注册
├── config.go            # 配置加载
├── database.go          # 数据库模型（GORM + SQLite）
├── account.go           # 账号轮询池（Round-Robin）
├── middleware.go         # 鉴权中间件
├── upstream.go           # 上游请求客户端（SSE）
├── handler_openai.go     # OpenAI 兼容端点
├── handler_anthropic.go  # Anthropic 兼容端点
├── handler_admin.go      # 管理面板 API
├── web/index.html        # 管理面板前端
├── Dockerfile
├── docker-compose.yml
└── README.md
```

## 技术栈

Go + Gin + GORM + SQLite

## Star History

[![GitHub Stars](https://img.shields.io/github/stars/Futureppo/codeflicke2api?logo=github&style=flat-square)](https://github.com/Futureppo/codeflicke2api/stargazers)

[![Star History Chart](https://api.star-history.com/svg?repos=Futureppo/codeflicke2api&type=Date)](https://star-history.com/#Futureppo/codeflicke2api&Date)
