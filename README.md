# 🚢 Host-Ship 自动续期工作流

公开运行 GitHub Actions 工作流，核心运行脚本存放于统一私有仓库 `my-private-scripts/host-ship` 中。
基于 DrissionPage + sing-box 节点代理实现多服务器自动续签、Cloudflare Turnstile 质询穿透、冷却时间 (CD) 自动检测等待与重试、失败/成功截图及 Telegram 通知推送。

## 配置说明

需要在本仓库的 **Settings -> Secrets and variables -> Actions** 中配置以下变量：

### 1. 凭据 Secrets (Repository Secrets)

| Secret 名称 | 说明 | 是否必填 |
| :--- | :--- | :--- |
| `CORE_SCRIPT_TOKEN` 或 `REPO_TOKEN` | 具备读取私有仓库 `my-private-scripts` 权限的 GitHub PAT | 必填 |
| `PANEL_USER` | Host-Ship 控制面板登录用户名 / 邮箱 | 必填 |
| `PANEL_PASS` | Host-Ship 控制面板登录密码 | 必填 |
| `TG_BOT_TOKEN` | Telegram Bot Token，用于发送续签通知与截图 | 选填 |
| `TG_CHAT_ID` | Telegram 接收通知的 Chat ID | 选填 |

### 2. 代理节点变量 (Repository Variables 或 Secrets)

通过加载 sing-box 运行代理通道，完美绕过 Cloudflare Turnstile 针对公共机房 IP 的质询阻断。可在 **Secrets** 或 **Variables** 中配置：

| 变量名称 | 说明 | 示例 |
| :--- | :--- | :--- |
| `PROXY_NODE` 或 `NODE_LINK` | 代理节点链接或 sing-box JSON 配置 | `hysteria2://...` / `vless://...` / `tuic://...` / `vmess://...` / `trojan://...` |

> 提示：支持填写单一节点链接，也支持多行或以逗号分隔填入多个候选备用节点（脚本将自动进行可用性检测并按顺序故障转移）。

## 手动触发测试

1. 打开本仓库的 **Actions** 页面。
2. 选择 **Host-Ship 续期** 工作流。
3. 点击 **Run workflow** 手动触发测试。
4. 之后每周日 00:00 (UTC) 自动定时执行。
