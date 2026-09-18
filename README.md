# 🚢 Host-Ship 自动续期工作流

公开运行 GitHub Actions 工作流，核心运行脚本存放于统一私有仓库 `my-private-scripts/host-ship` 中。
基于 DrissionPage 实现多服务器自动续签、冷却时间 (CD) 自动检测等待与重试、失败/成功截图及 Telegram 通知推送。

## 配置说明

需要在本仓库的 **Settings -> Secrets and variables -> Actions** 中配置以下 Secrets：

| Secret 名称 | 说明 | 是否必填 |
| :--- | :--- | :--- |
| `CORE_SCRIPT_TOKEN` 或 `REPO_TOKEN` | 具备读取私有仓库 `my-private-scripts` 权限的 GitHub Personal Access Token (PAT) | 必填 |
| `PANEL_USER` | Host-Ship 控制面板登录用户名 / 邮箱 | 必填 |
| `PANEL_PASS` | Host-Ship 控制面板登录密码 | 必填 |
| `TG_BOT_TOKEN` | Telegram Bot Token，用于发送续签通知与截图 | 选填 |
| `TG_CHAT_ID` | Telegram 接收通知的 Chat ID | 选填 |

## 手动触发测试

1. 打开本仓库的 **Actions** 页面。
2. 选择 **Host-Ship 续期** 工作流。
3. 点击 **Run workflow** 手动触发测试。
4. 之后每周日 00:00 (UTC) 自动定时执行。
