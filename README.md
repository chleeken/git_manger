# 🔧 Git 上传辅助工具（git_manger）

> 一个基于 **Python + Tkinter** 的单文件 Git 可视化辅助工具，零外部依赖、零配置文件，放在项目根目录双击即可使用。

---

## ✨ 核心特性

| 特性 | 说明 |
|------|------|
| 🛡️ **隐私文件强制过滤** | 代码层硬编码，永远不会被 `git add` 添加（`.env` / `.paml` / 密钥 / 点文件 / 构建产物） |
| 🖥️ **可视化 Git 操作** | `init` / `add` / `commit` / `remote` / `push` / `pull` / `status` / 分支管理，一键完成 |
| 🐙 **GitHub 一键建仓** | 支持 `gh CLI`（设备码登录）或 `curl + PAT Token` 自动创建远程仓库并推送 |
| 🤖 **GH007 自动修复** | 推送时检测 GitHub GH007 邮箱保护，自动改用 `noreply@users.noreply.github.com` 重提 |
| 📜 **自动生成 .gitignore** | 根据过滤规则自动生成/更新项目 `.gitignore` |
| 🧩 **自动拉取 + 推送** | 有未提交改动时自动 commit；远端领先时自动 `pull --rebase` 再推送 |
| 🎨 **多皮肤 + 暗黑模式** | 7 种亮色主题 + 暗黑模式，支持临时切换 |
| 🌐 **中英文切换** | 界面语言可一键切换 |
| 📦 **单文件** | 只有一个 `git_manger.py`，复制即用 |
| 🔑 **零外部依赖** | 纯标准库 `tkinter`，只需系统 Git |

---

## 📋 环境要求

- **Python** 3.10+（内置 `tkinter`）
- **Git** 已安装并加入系统 PATH（命令行能执行 `git --version`）
- **Windows / Linux / macOS** 均可

> 可选：
> - [GitHub CLI](https://cli.github.com/)（`gh` 命令）—— 用于一键建仓 + 设备码登录
> - `curl`（Windows 10+ 系统自带）—— 或用 PAT Token 走 GitHub REST API

---

## 🚀 快速开始

```bash
# 1. 把 git_manger.py 放到你的项目根目录（与 .git 同级）
# 2. 运行
python git_manger.py
```

Windows 下也可以直接双击 `.py` 文件（需已关联 Python）。

### 推荐工作流

```
🚀 初始化仓库 → 📦 扫描并添加 → ✍️ 代码提交
→ 🔗 远程仓库（粘贴 URL） → ⬆️ 推送到远程
```

---

## 📁 文件过滤规则（隐私保护）

本工具最核心的能力：**代码层强制拦截**，无论 `.gitignore` 如何配置，以下内容**永远不会**被 `git add` 添加上传：

### 强制黑名单（不可关闭）

| 类别 | 规则 |
|------|------|
| 固定文件名 | `git_manger.py`、`AGENTS.md`、`credentials.json`、`id_rsa` 等 |
| 敏感后缀 | `.env`、`.paml`、`.pyc`、`.log`、`.tmp`、`.bak`、`.db`、`.sqlite3`、`.ini`、`.token`、`.key`、`.pem`、`.crt`、`.pfx`、`.p12` 等 |
| 隐藏文件 | 所有 `.` 开头文件（`.gitignore` / `.gitattributes` 除外） |
| 忽略目录 | `chat_history/`、`tmp_uploads/`、`dist/`、`build/`、`.idea/`、`.vscode/`、`.git/`、`node_modules/`、`__pycache__/`、`.venv/` 等 |

### 自定义（永久生效）

编辑 `git_manger.py` **顶部**的【用户可修改配置区】，保存即可：

```python
FORCE_IGNORE_FILES = ["git_manger.py", "AGENTS.md", "你的秘密文件.json"]
FORCE_extra_suffixes = [".env", ".paml", ".你的后缀"]
FORCE_IGNORE_DIRS = ["chat_history", "dist", "build", "你的目录"]
EXTRA_extra_suffixes = [".bak", ".tmp"]
EXTRA_extra_names = ["credentials.json"]
```

### 自定义（临时，本次运行）

GUI → `🔑 Git 设置` 按钮里可以临时追加过滤后缀/文件名，关闭程序即失效。

---

## 🧭 界面说明

```
┌─────────────────────────────────────────────────────────────────────┐
│ 🔧 Git 上传辅助工具  [Git状态●] [Repo状态●]  📁 项目目录          │
│ [❓帮助] [ℹ️关于] [🌐EN] [🌙暗黑] [🎨皮肤]                          │
├─────────────────────────────────────────────────────────────────────┤
│ 📦 Git 操作                                                        │
│  [🚀 初始化] [📦 扫描添加] [✍️ 代码提交]                            │
│  [🔗 远程] [🌐 GitHub创建] [⬆️ 推送] [⬇️ 拉取]                       │
│                                                                     │
│ 🌿 分支管理                                                         │
│  [📋 列表] [➕ 创建] [🔀 切换] [➕ 合并]                            │
│                                                                     │
│ 🧹 其他                                                             │
│  [📊 状态] [📜 历史] [🔑 设置] [🔓 忽略] [📁 打开目录] [🔄 刷新]    │
│                                                                     │
│ ┌──────────────┐  ┌──────────────────────────────────────────────┐ │
│ │ 📁 项目文件   │  │ 🖥️ 操作日志              [📋 复制] [🧹 清空] │ │
│ │ (过滤后列表) │  │ git add ...                                  │ │
│ │ file1.py ✅  │  │ ✅ 执行成功                                    │ │
│ │ file2.py ✅  │  │                                               │ │
│ │ ...          │  │                                               │ │
│ └──────────────┘  └──────────────────────────────────────────────┘ │
├─────────────────────────────────────────────────────────────────────┤
│ ██████████████ 进度条                                                │
│ ✅ 就绪                                                             │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🐙 GitHub 建仓（两种方式）

### 方式 A：gh CLI + 设备码登录（推荐，最省事）

```bash
# 只需安装 gh CLI：
winget install GitHub.cli     # Windows
brew install gh               # macOS
sudo apt install gh            # Linux (或自己去 github.com/cli/cli/releases 下)
```

然后点 `🌐 GitHub创建` → 点 `gh login` → 浏览器里输入设备码授权即可。工具会自动：
1. 解析 `gh auth login --web` 输出的一次性验证码
2. 打开浏览器让你授权
3. 登录成功后自动 `gh repo create` + 推送上远程

### 方式 B：curl + PAT Token（不装任何额外工具）

点 `🌐 GitHub创建`，在 PAT Token 输入框粘贴一个 `repo` 权限的 Personal Access Token：

> GitHub → Settings → Developer settings → Personal access tokens → Generate new token (classic)，勾选 `repo` 即可。

Token 仅在**当前 GUI 会话**有效，**不会**被保存到磁盘。

### 仓库创建后自动推送

无论哪种方式，建仓成功后工具都会：
- 如果本地还没有 commit：自动 `add` + `commit`（含 `.gitignore`）
- 自动设置远端 `origin`
- 自动 `push -u origin <branch>`
- 自动修复 GH007（隐私邮箱保护）—— 如果推送被拒，会自动切换到 `@users.noreply.github.com`

---

## 🛡️ GH007 隐私邮箱自动修复

GitHub 会拒绝用个人邮箱（163/qq/gmail/outlook/yahoo/hotmail）提交的公开仓库（或有公开贡献的仓库），错误信息类似：

```
GH007: We found an email address in your commits that does not match
any of the email addresses on your GitHub account...
```

工具内置了自动处理：

1. 推送时如果捕获到 GH007 提示
2. 自动 `git config --global user.email` 设为 `<用户名>@users.noreply.github.com`
3. 自动 `git commit --amend --reset-author --no-edit`
4. 自动 `git push --force-with-lease` 重试
5. 推送成功 ✅

---

## 🧹 自动 .gitignore + 清理已跟踪隐私文件

首次初始化或推送时，工具会自动：

1. 在项目根目录写入一个 **git_manger.py 自己维护的** `.gitignore`（包含所有过滤规则 + Python/Node/IDE/构建产物）
2. 扫描 Git index 中已被追踪但命中过滤规则的文件（如之前误提交的 `.env`、`chat_history/`），执行 `git rm --cached` 停止追踪（**不删本地文件**）

---

## 📄 目录结构

```
git_manger/
├── git_manger.py        ← 主程序（所有代码都在这个文件里）
├── icon.ico             ← 可选：窗口图标
├── _fix_add.py          ← 历史补丁脚本
├── _patch_push_check.py ← 历史补丁脚本
├── __pycache__/
└── README.md
```

---

## 🔧 技术说明

- **语言**: Python 3.10+
- **GUI**: Tkinter（标准库）
- **Git 调用**: `subprocess.run(["git", ...], ...)` 封装系统 Git，零依赖
- **线程模型**: Git 操作放 `threading.Thread`，GUI 不卡顿
- **跨平台**: 路径自动 `os.sep` → `/` 转换；Windows 控制台 UTF-8 兼容
- **打包**: 可以用 PyInstaller / Nuitka 打成单文件 `.exe`，程序用 `_safe_get_real_executable()` 自动判断运行时目录

### 核心源码结构

```
git_manger.py
├── 顶部【用户可修改配置区】  # 改完保存，永远不改其他代码
├── 基础路径 / 日志
├── Git 命令封装 run_git()
├── 文件过滤 is_ignored() + scan_project_files()
├── 运行时配置 make_runtime_cfg()
├── 主题 / Tooltip / 粘贴对话框
├── GitHub noreply 邮箱 GH007 修复
├── 自动 .gitignore + prune 已追踪隐私文件
└── GitManagerApp(tk.Tk)   ← 所有 GUI 和操作入口
```

---

## ❓ 常见问题

**Q: 为什么 Python 报错 `ModuleNotFoundError: No module named 'tkinter'`？**
A: 你装的是精简版 Python。重装官方完整版（python.org）或 Windows Store 版，自带 tkinter。Linux 下：`sudo apt install python3-tk`。

**Q: 推送失败 `fatal: remote origin already exists`？**
A: 本工具已做了兼容——绑定远程时会先 `git remote remove origin` 再加，不会再报。

**Q: PAT Token 会被保存吗？**
A: 不会。仅存在当前 GUI 会话内存里，程序关闭即消失。

**Q: 工具能打包成 exe 吗？**
A: 能。`pyinstaller -F -w git_manger.py` 或 Nuitka 都行，`_safe_get_real_executable()` 会自动识别 PyInstaller/Nuitka 可执行文件路径。

**Q: 隐私文件已被提交过怎么办？**
A: 推送到远程前，工具会自动 `git rm --cached` 把命中过滤规则的已跟踪文件从 Git 索引里移除（本地文件不删），确保下一次 push 不再包含它们。

**Q: 规则改了但界面没变？**
A: 改了文件顶部配置区后，重启程序即可。设置里的临时规则点 `💾 应用（本次运行）` 即可。

---

## 📄 许可证

本项目为内部工具，遵循项目根目录的开源许可。请遵守 GitHub 用户协议与相关法律法规。
